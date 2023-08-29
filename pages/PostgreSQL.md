- ## Function Language
	- [plpgsql](https://de.wikipedia.org/wiki/PL/pgSQL)
		- https://www.postgresql.org/docs/14/plpgsql.html
		- PostgreSQL  Error Codes
			- https://www.postgresql.org/docs/current/errcodes-appendix.html
	- ``` sql
	  
	  do $$
	  
	  declare 
	  	v_nickname_result text;
	  begin
	  	insert into players(auth_identity, nickname) values ('d2d6a325-007e-4ce3-af94-e60eb954ee13', 'Aiminh')
	  			on conflict (auth_identity) do update set auth_identity = 'd2d6a325-007e-4ce3-af94-e60eb954ee13', nickname ='Aiminh' 
	  			
	  			returning nickname into v_nickname_result;
	  		
	  exception 
	  	WHEN unique_violation then 
	  end;
	  $$ language plpgsql
	  
	  
	  ```
		-
- ## Tools
	- GUI
		- [DBeaver](https://dbeaver.io/) install via [[Chocolatey]]
-
-