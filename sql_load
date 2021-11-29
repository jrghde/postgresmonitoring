-- Tabelle erstellen 
CREATE TABLE checkmk_load(
  id SERIAL,
  idcntr int,
  rndstr varchar(255),
  uuid varchar(64),
  tstamp varchar(32)
);

-- Daten einfügen und löschen
DO $$
declare
  DEBUG CONSTANT boolean := true;
  maxcntr CONSTANT integer := 100000000;
  rndcntr CONSTANT integer := 17;
  randomstr character varying(255);
  uuid character varying(64);
  stamp character varying(32);
  deletenow integer;
  todelete integer;
  deletedcntr integer;
  insertedcntr integer;
begin
deletedcntr := 1;
insertedcntr := 1;
FOR cntr IN 1..maxcntr 
	LOOP
		SELECT md5(random()::text) into randomstr;
    	SELECT uuid_in(md5(random()::text || clock_timestamp()::text)::cstring) into uuid;
    	SELECT CURRENT_TIMESTAMP into stamp;
    	SELECT floor(random() * 999 + 1)::int into deletenow;
    	SELECT floor(random() * (cntr-1) + 1)::int into todelete;
    	INSERT INTO checkmk_load(idcntr, rndstr, uuid, tstamp) values(cntr, randomstr, uuid, stamp);
        insertedcntr := insertedcntr + 1;
        if DEBUG then
          --raise notice 'Inserted record: %', cntr;
          if MOD(cntr,1000) = 0 then
            raise notice 'Total inserted records: %', insertedcntr;
           end if;
        end if;
        IF deletenow = rndcntr then
          delete from checkmk_load where id = todelete;
          deletedcntr := deletedcntr + 1;
          if DEBUG then
            --raise notice 'Deleted record: %', todelete;
            raise notice 'Total deleted records: %', deletedcntr;
          end if;
        end if;
--    	commit;
	end loop;
end $$;

-- Anzahl Records bestimmen
SELECT count(*) FROM checkmk_load;

-- Records anzeigen
select * from checkmk_load;


-- Tabelle leeren
truncate table checkmk_load;

-- Tabelle vollständig löschen
drop table checkmk_load;
