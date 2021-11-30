# postgresmonitoring
PostgreSQL Monitoring with CheckMK (Docker environment)

mk_postgres.py - Anpassungen für Host-Kommunikation 

  Damit das Check Script für PostgreSQL richtig funktioniert, muss noch ein .pgpass File im Homeverzeichnis des Benutzers postgres angelegt werden:  
  
    localhost:5432:postgres:postgres:zli12345  
    
    Das .pgpass File muss zwingend die folgenden Berechtigungen haben  
    
        -rw------- 1 postgres postgres   42 Nov 25 20:38 .pgpass  

Link zu Noah Geelers docker-compose File: <https://github.com/Nevah5/DockerMonitoring>
