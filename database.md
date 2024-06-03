```
from sqlmodel import Field, Session, SQLModel, create_engine, select, Sequence
```

Step_01# make class with SQL Modal
```
class Todo(SQLModel, table=True):
    id: Optional[int] = Field(default=None, primary_key=True)
    content: str = Field(index=True)
```
Step_02# make database connection string
```
# only needed for psycopg 3 - replace postgresql
# with postgresql+psycopg in settings.DATABASE_URL
connection_string = str(settings.DATABASE_URL).replace(
    "postgresql", "postgresql+psycopg"
)

```
step03# create engine and pass db connection string in it
```
# only needed for psycopg 3 - replace postgresql
# with postgresql+psycopg in settings.DATABASE_URL
engine = create_engine(
    connection_string, connect_args={}, pool_recycle=300
)

```
step04# create fuction and pass engine to it 

```
def create_db_and_tables()->None:
    SQLModel.metadata.create_all(engine)
```
step05 # create session function using engine

```
def get_session():
    with Session(engine) as session:
        yield session
```
