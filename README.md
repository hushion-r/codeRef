# Code Reference

## General To-Know

### Code not working?
- [Address already in use](#address-already-in-use)
- [React Random Things I’ve Gotten Weird](#random-things-ive-gotten-weird)
- [Backend Random Things I’ve Gotten Weird](#backend-random-things-ive-gotten-weird)

### Workarounds
When making new accounts, do email+etc@compozelabs.com, and it will register as diff email but send to main email

### Package
major.minor.patch

## CLI

#### Address already in use
```sh
lsof -i tcp:4000
```
```sh
kill -9
```

### Git

#### Rebase
```sh
git pull -r
```

#### Branch
```sh
git branch [[branch name]]
```
```sh
git pull
```
```sh
git stash
```
```sh
git switch [[branch name]]
```
```sh
git merge master
```

Cleanup
```sh
git fetch —prune
```
```sh
git branch -a
```
```sh
git remote prune origin
```

### React

#### App
```bash
npm run clean-start
npm run [[android, ios]]
```

#### Installing packages
You can install a particular version of the library by running `npm i <library-name>@<version-number>`
```bash
?
npm i … prop-types
```
Import types `@types/packageName`
```sh
npm i --save-dev @types/
```

### Storybook
```bash
npm run storybook
```
```bash
npm run storyshots
```

### Docker
i.e. `docker build . -t fca:local`
```bash
docker build . -t name:tag
```

## React Code

### Random Things I’ve Gotten Weird
- Must have `display: flex` to properly use all flex properties
- Must have `{...register}` as last item in `<Input />`
- `let listToSort = [...immutableList];`
- Must have redux function in dispatch
- Don’t put dispatch in render
- Make sure backend imports are correct
- “varchar” vs “int”
- `await`
- State not changing but console.log running? Check if changing twice

### Code Tidbits

#### Console.log()
```js
console.log('\n\n\n\n\n\n\n\n\n\n\n\n\n\n\n');
```

#### Sort alphabetically
```js
.sort((a, b) => a.name.localeCompare(b.name))
```

#### Filter out `isDeleted`
Replace `obj`
```js
.filter((obj) => !obj.isDeleted)
```

#### Map
Replace `obj`. Make sure to add `key={}` with some unique value, usually ``${obj.name} ${i}`` (in backticks, can't make markdown work rn)
```js
.map((obj, index: number) => return {})
```

### Hooks
Must always be used in root level of functional component

```tsx
interface ComponentProps { var: Type; }
export const Component = ( { var }: ComponentProps ): JSX.Element => { return (<></>)}
 
export const Component = (): JSX.Element => { return (<></>) }
```

#### useState
```tsx
import { useState } from 'react';
```
`const [val, setVal] = useState<type>(initialVal);`
```tsx
const [, set] = useState<>();
```

#### useEffect
```tsx
import { useEffect } from 'react';
```
`useEffect(() => {action}, [trigger]);`
```tsx
useEffect(() => {}, []);
```

#### React Hook Forms
```tsx
interface xParams {
 x: type;
}
 
const { register, handleSubmit, formState: { errors }, } = useForm<xParams>();
 
const xNameRegister = register(X_NAME_KEY);
 
const onSubmit = async (data: xParams): Promise<void> => {}
 
<form onSubmit={handleSubmit(onSubmit)}>
    <Input {...xNameRegister} />
    <Button type='submit'></Button>
</form>
 
const X_NAME_KEY = 'xName';
```

### Redux
useAppDispatch
```ts
const dispatch = useAppDispatch();
```

useAppSelector

`const currentUser: UserData | undefined = useAppSelector(selectUserData);`

```ts
const current:  | undefined = useAppSelector(select);
```

## Backend

### Code Tidbits

#### Relations
```ts
relations: [''],
```

#### Where
```ts
where: { id: Id, isDeleted: true }
```

## SQL
```sql
UPDATE [master].[dbo].[user_entity] SET is_admin = 1 WHERE email = 'rae@compozelabs.com'
```
```sql
UPDATE [master].[dbo].[user_entity] SET [eula] = 0
```
Can use `like` instead of `=`
```sql 
INSERT INTO [master].[dbo].[user_entity] ([first_name], [last_name], [email], [user_type], [job_title], [phone_number], [eula]) VALUES ('Rae', 'H', 'rae@compozelabs.com', 'admin', 'dev', '555.555.5555', 0)
```

## Database

### Backend Random Things I've Gotten Weird

#### Trying to get entity from join column that have just dropped
Refresh server

#### Test working but API calls not?
Make sure you have the value in relations in the service file

#### Getting HTML back instead of an object?
Try rebuilding and checking that you're cealling the right URL.

#### Can't reach the request URL? {message": "Not Found"} ?
Check imports for controllers.

#### Creating a new thing removes the relations of the old thing to the parent?
Check relations/get. Check eager.

#### Site stopped working? But works on local?
Make sure you drop changed tables from the environment then restart from the portal.

#### Can do some saves but not others?
Check allowed columnn length.

### Add SQL Server Connection
Open `database.config.ts`

## Deploy

### Deploy to TestFlight
1. Check iOS on dev server
2. App Store Connect, check for version + build
3. Xcode
4. Click folder icon in top left. Click on app folder
5. Go to General tab, change version + build
6. Product ==> Archive
7. If fail, go to Build Phases ==> Copy Bundle Resources, delete certain fonts
8. Click through defaults
9. App Store Connect, click No

### Azure
1. ``` npm run build dev/production ```
2. Scripts > deploy.sh
3. Uncomment `az acr build --registry containername --image portalimage .`  
4. ``` npm run deploy dev ```
5. Go to [Azure Portal](https://portal.azure.com/#home)
6. Diagnose and Solve Problems
7. Availability & Performance
8. Application logs
9. Platform logs

