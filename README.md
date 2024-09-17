# sikach

Sikach is an SQL dialect that allows you to write any application you can write with other languages. 

## Roadmap 

We are probably talking about decades here.

 - [ ] Compilation
   - [ ] Interpreter in C++
   - [ ] Interpreter in Sikach
   - [ ] JIT Compiler in C++
   - [ ] JIT Compiler in Sikach
   - [ ] Compiler in C++
   - [ ] Compiler in Sikach
 - [ ] Database
   - [ ] In memory database
   - [ ] Persistent database
   - [ ] Indexing
   - [ ] Scaling database
 - [ ] Packages
   - [ ] Local
   - [ ] Remote
 - [ ] UI framework
 - [ ] Tooling

## Language design

The end goal of the project is to have the following code:

```sql
CREATE TABLE todo (
    id int NOT NULL AUTO_INCREMENT,
    item TEXT NOT NULL,
);

CREATE VIEW todo_screen AS
    SELECT ui_column(
        SELECT ui_row(
            ui_text(text = item),
            ui_button(
                text = "Delete",
                on_click = () => delete(id),
            ),
        )
        FROM todo
        UNION
        SELECT ui_row(
            ui_text_edit(
                id = "add_new_todo",
            ),
            ui_button(
                text = "Add",
                on_click = () => insert(ui_find_element("add_new_todo").text),
            ),
        )
    )
;

insert:
INSERT INTO todo (item)
VALUES (:item)
;

delete:
DELETE FROM todo
WHERE id = (:id)
;
```

Compile into two artifacts server and client. Client will have UI and server will host a database and will push data to the client as well as accept insert and delete requests from the client.
