# mssql-server-linux-tools
Docker image for building MSSQL Server with mssql-tools

Running the image
--
`docker run -e 'SA_PASSWORD=[strongPassw0rd!]' -p 1433:1433 --name mssql -d taylorbarrick/mssql-server-linux-tools`
  
Adding Primer Script
--

`FROM taylorbarrick/mssql-server-linux-tools`  
`ENV MSSQL_DB=CoolDB`  
`ENV MSSQL_USER=Tester`  
`ENV MSSQL_PASSWORD=Test1234`  
`ADD entrypoint.sh / `  
`ADD init.sql /opt/mssql/`  
`RUN chmod +x /entrypoint.sh`  
`ENTRYPOINT ["/entrypoint.sh"]`  

Including a call to sqlcmd within entrypoint.sql to 
execute the sql file, but only after ensuring that the engine 
is up and running.  (Sometimes takes as mucgh as 45 seconds)
