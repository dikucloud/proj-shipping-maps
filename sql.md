select st_numpoints(linestring) from ways limit 10;

select sum(st_numpoints(linestring)) from ways;

select sum(st_numpoints(st_simplify(linestring, 0.01))) from ways;

select count(linestring) from ways;

select st_astext(linestring) from ways limit 1;

select max(st_numpoints(linestring)), st_isring(linestring) as isring, count(st_isring(linestring)) from ways group by st_isring(linestring);

select sum(st_numpoints(linestring)) from ways;

-- http://georepository.com/crs_3189/GR96-UTM-zone-29N.html
select sum(st_numpoints(st_transform(linestring,3189))) from ways;
select sum(st_numpoints(st_simplify(st_transform(linestring,3189), 1))) from ways;
select sum(st_numpoints(st_simplify(st_transform(linestring,3189), 25))) from ways;
select sum(st_numpoints(st_simplify(st_transform(linestring,3189), 100))) from ways;
select sum(st_numpoints(st_simplify(st_transform(linestring,3189), 500))) from ways;

select min(st_numpoints(linestring)) from ways;
select min(st_numpoints(st_simplify(st_transform(linestring,3189), 1))) from ways;

select st_numpoints(linestring) as before, st_numpoints(st_simplify(st_transform(linestring,3189), 25)) as after, st_area(st_makepolygon(st_transform(linestring,3189))) as area from ways where st_numpoints(st_simplify(st_transform(linestring,3189), 25)) = 1 and st_isring(linestring);


select min(st_area(st_makepolygon(st_transform(linestring,3189)))) from ways where st_isring(linestring);