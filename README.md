# api_adonis
Create an API to use in Insterest project -> an Angular project that I working on

* start your project with the following commands
```
npm init adonis-ts-app@latest .
```
![adonis installation command](images/install.png "adonis installation command").

* Choose te API option
* Answer true for the **eslint** and **prettier** extensions.

At the end of this installation, use the following command to run your Adonis API:

```
node ace serve --watch
```
The usual adress of the API is the localhost:3333. Access to visualize the following message on your browser:

```
{
  "hello": "world"
}
```
## Install lucid ORM

```
npm i @adonisjs/lucid
```
Now we need to configure lucid:
```
node ace configure @adonisjs/lucid
```
Choose the **SQLite** database and **In the terminal** option after the  installation is complete.

Configure **cors.ts** file at **config** directory.

```
enabled: (request) => request.url().startsWith('/api'),

```
Now we have access to URLs that starts with **/api**.
Modify your **routes.ts** file:

```
Route.group(() => {
  Route.get('/', async () => {
    return { hello: 'world' }
  })
}).prefix('/api')
```
We need to create an architecture based on database.

Next step: we will create an API to save moments of your life, with photos, comments, date, ...
When you type the following command on terminal, you receive a list of actions that ADONIS can make:

```
node ace
```

Start using this command on terminal to use Adonis to create the Model directory:

```
node ace make:model Moment -m
```
Open the created file Moments.ts:

```
import { DateTime } from 'luxon'
import { BaseModel, column } from '@ioc:Adonis/Lucid/Orm'

export default class Moment extends BaseModel {
  @column({ isPrimary: true })
  public id: number

  @column.dateTime({ autoCreate: true })
  public createdAt: DateTime

  @column.dateTime({ autoCreate: true, autoUpdate: true })
  public updatedAt: DateTime
}
```
This file contains 3 columns of the database and we will add 3 more:

```
@column()
  public title: string

  @column()
  public description: string

  @column()
  public image: string
```
At the next step, we have to reflect this changes on **migrations/** file, adding the 3 new columns to it.

```
table.string('title')
table.string('description')
table.string('image')
```
Run the command on terminal:
```
node ace migration:run
```
Notice that this command create a temporary database on **tmp** directory.
