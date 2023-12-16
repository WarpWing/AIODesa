# Asyncio Dead Easy Sql API

## Simplify Your Personal Projects with AIODesa

### Are you tired of the hassle of setting up complex databases for your personal projects? AIODesa is the solution! Designed with developer experience in mind, AIODesa makes managing asynchronous database access a breeze, perfect for smaller-scale applications where extensive database operations are not a priority.

### *No need to write even a single line of raw SQL.*

AIODesa offers a straightforward and 100% Python interface for managing asynchronous database access. By leveraging Python's built-ins and standard library, it seamlessly wraps around AioSqlite, providing a hassle-free experience. With AIODesa, you can define, generate, and commit data effortlessly, thanks to shared objects for tables and records.


### Ideal for Personal Projects

AIODesa is specifically crafted for simpler projects where database IO is minimal. It's not intended for heavy production use but rather serves as an excellent choice for personal projects that require data persistence without the complexity of a full-scale database setup. SQLite is leveraged here, meaning youre free to use other SQLite drivers to consume and transform the data if your project outgrows AIODesa.

Whether you're working on a hobby project or a small personal application, AIODesa streamlines the process, allowing you to focus on your ideas rather than intricate database configurations.


![AIODesa](https://github.com/sockheadrps/AIODesa/blob/main/AIODesaEx1.png?raw=true)

# Usage

__Install via pip__
```
pip install aiodesa
```

Sample API usage:

```
from aiodesa import Db
import asyncio
from dataclasses import dataclass
from aiodesa.utils.tables import ForeignKey, UniqueKey, PrimaryKey, set_key


async def main():
	# Define structure for both tables and records
	# Easily define key types
	@dataclass
	@set_key(PrimaryKey("username"), UniqueKey("id"), ForeignKey("username", "anothertable"))
	class UserEcon:
		username: str
		credits: int | None = None
		points: int | None = None
		id: str | None = None
		table_name: str = "user_economy"


	async with Db("database.sqlite3") as db:
		# Create table from UserEcon class
		await db.read_table_schemas(UserEcon)

		# Insert a record
		record = db.insert(UserEcon.table_name)
		await record('sockheadrps', id="fffff")

		# Update a record
		record = db.update(UserEcon.table_name, column_identifier="username")
		await record('sockheadrps', points=2330, id="1234")
		

asyncio.run(main())

```

<br>

# Development:

Ensure poetry is installed:

```
pip install poetry
```

Install project using poetry

```
poetry add git+https://github.com/sockheadrps/AIODesa.git
poetry install
```

create a python file for using AIODesa and activate poetry virtual env to run it

```
poetry shell
poetry run python main.py
```
