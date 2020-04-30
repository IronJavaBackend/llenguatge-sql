# Llenguatge-sql

### Consultas sobre una tabla

### 1. Lista el nombre de todos los productos que hay en la tabla `producto` .
```bash
> SELECT nombre FROM producto;
```

### 2. Lista los nombres y los precios de todos los productos de la tabla` producto`.
```bash
> SELECT nombre, precio FROM producto;
```

### 3. Lista todas las columnas de la tabla `producto`.
```bash
> SELECT * FROM producto;
```

### 4. Lista el nombre de los productos, el precio en euros y el precio en dólares estadounidenses (USD).
```bash
> SELECT nombre, CONCAT(precio,'€'), CONCAT((precio * 1.083),'$') FROM producto;
```

### 5. Lista el nombre de los productos, el precio en euros y el precio en dólares estadounidenses (USD). Utiliza los siguientes alias para las columnas: nombre de producto, euros, dólares.
```bash
> SELECT nombre AS 'nombre de producto', precio AS 'euros', (precio * 1.083) AS 'dólares' FROM producto;
```

### 6. Lista los nombres y los precios de todos los productos de la tabla `producto`, convirtiendo los nombres a mayúscula.
```bash
> SELECT UPPER(nombre), precio FROM producto;
```

### 7. Lista los nombres y los precios de todos los productos de la tabla `producto`, convirtiendo los nombres a minúscula.
```bash
> SELECT LOWER(nombre), precio FROM producto;
```

### 8. Lista el nombre de todos los fabricantes en una columna, y en otra columna obtenga en mayúsculas los dos primeros caracteres del nombre del fabricante.
```bash
> SELECT nombre, UPPER(LEFT(nombre, 2)) FROM fabricante;
```

### 9. Lista los nombres y los precios de todos los productos de la tabla `producto`, redondeando el valor del precio.
```bash
> SELECT nombre, ROUND(precio,0) FROM producto;
```

### 10. Lista los nombres y los precios de todos los productos de la tabla `producto`, truncando el valor del precio para mostrarlo sin ninguna cifra decimal.
```bash
> SELECT nombre, precio, TRUNCATE(precio,0) FROM producto;
```

### 11. Lista el código de los fabricantes que tienen productos en la tabla `producto`.
```bash
> SELECT codigo_fabricante FROM producto;
```

### 12. Lista el código de los fabricantes que tienen productos en la tabla `producto`, eliminando los códigos que aparecen repetidos.
```bash
> SELECT DISTINCT(codigo_fabricante) FROM producto;
```

### 13. Lista los nombres de los fabricantes ordenados de forma ascendente.
```bash
> SELECT nombre FROM fabricante ORDER BY nombre ASC;
```

### 14. Lista los nombres de los fabricantes ordenados de forma descendente.
```bash
> SELECT nombre FROM fabricante ORDER BY nombre DESC;
```

### 15. Lista los nombres de los productos ordenados en primer lugar por el nombre de forma ascendente y en segundo lugar por el precio de forma descendente.
```bash
> SELECT nombre FROM producto ORDER BY nombre DESC;
```

### 16. Devuelve una lista con las 5 primeras filas de la tabla `fabricante`.
```bash
> SELECT * FROM fabricante LIMIT 5;
```

### 17. Devuelve una lista con 2 filas a partir de la cuarta fila de la tabla `fabricante`. La cuarta fila también se debe incluir en la respuesta.
```bash
> SELECT * FROM fabricante LIMIT 2,2;
```

### 18. Lista el nombre y el precio del producto más barato. (Utilice solamente las cláusulas ORDER BY y LIMIT).
```bash
> SELECT nombre, precio FROM producto ORDER BY precio ASC LIMIT 1;
```

### 19. Lista el nombre y el precio del producto más caro. (Utilice solamente las cláusulas ORDER BY y LIMIT).
```bash
> SELECT nombre, precio FROM producto ORDER BY precio DESC LIMIT 1;
```

### 20. Lista el nombre de todos los productos del fabricante cuyo código de fabricante es igual a 2.
```bash
> SELECT nombre FROM producto WHERE codigo_fabricante = 2;
```

### 21. Lista el nombre de los productos que tienen un precio menor o igual a 120€.
```bash
> SELECT nombre FROM producto WHERE precio <= 120;
```

### 22. Lista el nombre de los productos que tienen un precio mayor o igual a 400€.
```bash
> SELECT nombre FROM producto WHERE precio >= 400;
```

### 23. Lista el nombre de los productos que no tienen un precio mayor o igual a 400€.
```bash
> SELECT nombre FROM producto WHERE precio < 400;
```

### 24. Lista todos los productos que tengan un precio entre 80€ y 300€. Sin utilizar el operador BETWEEN.
```bash
> SELECT * FROM producto WHERE precio >= 80 AND precio <= 300;
```

### 25. Lista todos los productos que tengan un precio entre 60€ y 200€. Utilizando el operador BETWEEN.
```bash
> SELECT * FROM producto WHERE precio BETWEEN 80 AND 300;
```

### 26. Lista todos los productos que tengan un precio mayor que 200€ y que el código de fabricante sea igual a 6.
```bash
> SELECT * FROM producto WHERE precio > 200 AND codigo_fabricante = 6;
```

### 27. Lista todos los productos donde el código de fabricante sea 1, 3 o 5. Sin utilizar el operador IN.
```bash
> SELECT * FROM producto WHERE codigo_fabricante = 1 OR codigo_fabricante = 3 OR codigo_fabricante = 5;
```

### 28. Lista todos los productos donde el código de fabricante sea 1, 3 o 5. Utilizando el operador IN.
```bash
> SELECT * FROM producto WHERE codigo_fabricante IN (1,3,5);
```

### 29. Lista el nombre y el precio de los productos en céntimos (Habrá que multiplicar por 100 el valor del precio). Cree un alias para la columna que contiene el precio que se llame céntimos.
```bash
> SELECT nombre, precio, precio*100 AS "céntimos" FROM producto;
```

### 30. Lista los nombres de los fabricantes cuyo nombre empiece por la letra S.
```bash
> SELECT nombre FROM fabricante WHERE nombre REGEXP "^S";
```

### 31. Lista los nombres de los fabricantes cuyo nombre termine por la vocal e.
```bash
> SELECT nombre FROM fabricante WHERE nombre LIKE "%e";
```

### 32. Lista los nombres de los fabricantes cuyo nombre contenga el carácter w.
```bash
> SELECT nombre FROM fabricante WHERE nombre LIKE "%w%";
```

### 33. Lista los nombres de los fabricantes cuyo nombre sea de 4 caracteres.
```bash
> SELECT nombre FROM fabricante WHERE CHARACTER_LENGTH(nombre) = 4;
```

### 34. Devuelve una lista con el nombre de todos los productos que contienen la cadena Portátil en el nombre.
```bash
> SELECT nombre FROM producto WHERE nombre LIKE '%Portátil%';
```

### 35. Devuelve una lista con el nombre de todos los productos que contienen la cadena Monitor en el nombre y tienen un precio inferior a 215 €.
```bash
> SELECT nombre FROM producto WHERE nombre LIKE '%Monitor%' AND precio < 215;
```

### 36. Lista el nombre y el precio de todos los productos que tengan un precio mayor o igual a 180€. Ordene el resultado en primer lugar por el precio (en orden descendente) y en segundo lugar por el nombre (en orden ascendente).
```bash
> SELECT nombre, PRECIO FROM producto WHERE precio >= 180 ORDER BY precio DESC, nombre ASC;
```


### Consultas multitabla (Composición interna)

### 1. Devuelve una lista con el nombre del producto, precio y nombre de fabricante de todos los productos de la base de datos.
```bash
> SELECT p.nombre, p.precio, f.nombre AS 'nombre del fabricante' FROM producto p JOIN fabricante f ON p.codigo_fabricante = f.codigo;
```

### 2. Devuelve una lista con el nombre del producto, precio y nombre de fabricante de todos los productos de la base de datos. Ordene el resultado por el nombre del fabricante, por orden alfabético.
```bash
> SELECT p.nombre, p.precio, f.nombre AS 'nombre del fabricante' FROM producto p JOIN fabricante f ON p.codigo_fabricante = f.codigo ORDER BY f.nombre ASC;
```

### 3. Devuelve una lista con el código del producto, nombre del producto, código del fabricante y nombre del fabricante, de todos los productos de la base de datos.

```bash
> SELECT p.codigo AS 'codigo de producto', p.nombre AS 'nombre de producto', f.codigo 'codigo del fabricante', f.nombre AS 'nombre del fabricante' FROM producto p JOIN fabricante f ON p.codigo_fabricante = f.codigo;
```

### 4. Devuelve el nombre del producto, su precio y el nombre de su fabricante, del producto más barato.
```bash
SELECT p.nombre AS 'nombre de producto', p.precio AS 'precio de producto', f.nombre AS 'nombre del fabricante' 
FROM producto p 
JOIN fabricante f ON p.codigo_fabricante = f.codigo 
ORDER BY p.precio ASC 
LIMIT 1;
```

### 5. Devuelve el nombre del producto, su precio y el nombre de su fabricante, del producto más caro.
```bash
SELECT p.nombre AS 'nombre de producto', p.precio AS 'precio de producto', f.nombre AS 'nombre del fabricante' 
FROM producto p 
JOIN fabricante f ON p.codigo_fabricante = f.codigo 
ORDER BY p.precio DESC
LIMIT 1;
```

### 6. Devuelve una lista de todos los productos del fabricante Lenovo.
```bash
SELECT p.nombre AS 'nombre de producto', p.precio AS 'precio de producto', f.nombre AS 'nombre del fabricante' 
FROM producto p 
JOIN fabricante f ON p.codigo_fabricante = f.codigo 
WHERE f.nombre = 'Lenovo';
```

### 7. Devuelve una lista de todos los productos del fabricante Crucial que tengan un precio mayor que 200€.
```bash
SELECT p.nombre AS 'nombre de producto', p.precio AS 'precio de producto', f.nombre AS 'nombre del fabricante' 
FROM producto p 
JOIN fabricante f ON p.codigo_fabricante = f.codigo 
WHERE f.nombre = 'Crucial' 
AND p.precio > 200;
```

### 8. Devuelve un listado con todos los productos de los fabricantes Asus, Hewlett-Packardy Seagate. Sin utilizar el operador IN.
```bash
SELECT p.nombre AS 'nombre de producto', p.precio AS 'precio de producto', f.nombre AS 'nombre del fabricante' 
FROM producto p 
JOIN fabricante f ON p.codigo_fabricante = f.codigo 
WHERE f.nombre = 'Asus' OR f.nombre = 'Hewlett-Packard'  OR f.nombre = 'Seagate';
```

### 9. Devuelve un listado con todos los productos de los fabricantes Asus, Hewlett-Packardy Seagate. Utilizando el operador IN.
```bash
SELECT p.nombre AS 'nombre de producto', p.precio AS 'precio de producto', f.nombre AS 'nombre del fabricante' 
FROM producto p 
JOIN fabricante f ON p.codigo_fabricante = f.codigo 
WHERE f.nombre in ('Asus', 'Hewlett-Packard', 'Seagate');
```

### 10. Devuelve un listado con el nombre y el precio de todos los productos de los fabricantes cuyo nombre termine por la vocal e.
```bash
SELECT p.nombre AS 'nombre de producto', p.precio AS 'precio de producto' 
FROM producto p 
JOIN fabricante f ON p.codigo_fabricante = f.codigo 
WHERE f.nombre LIKE '%e';
```

### 11. Devuelve un listado con el nombre y el precio de todos los productos cuyo nombre de fabricante contenga el carácter w en su nombre.
```bash
SELECT p.nombre AS 'nombre de producto', p.precio AS 'precio de producto' 
FROM producto p 
JOIN fabricante f ON p.codigo_fabricante = f.codigo 
WHERE f.nombre LIKE '%w%';
```

### 12. Devuelve un listado con el nombre de producto, precio y nombre de fabricante, de todos los productos que tengan un precio mayor o igual a 180€. Ordene el resultado en primer lugar por el precio (en orden descendente) y en segundo lugar por el nombre (en orden ascendente)
```bash
SELECT p.nombre AS 'nombre de producto', p.precio AS 'precio de producto', f.nombre AS 'nombre de fabricante'
FROM producto p 
JOIN fabricante f ON p.codigo_fabricante = f.codigo 
WHERE p.precio >= 180
ORDER BY p.precio DESC, p.nombre ASC;
```

### 13. Devuelve un listado con el código y el nombre de fabricante, solamente de aquellos fabricantes que tienen productos asociados en la base de datos.
```bash
SELECT f.codigo AS 'codigo de fabricante', f.nombre AS 'nombre de fabricante'
FROM fabricante f 
WHERE f.codigo IN (SELECT DISTINCT(codigo_fabricante) FROM producto);
```

### Consultas multitabla (Composición externa)
## Resuelva todas las consultas utilizando las cláusulas LEFT JOIN y RIGHT JOIN.

### 1. Devuelve un listado de `todos los fabricantes` que existen en la base de datos, junto con los productos que tiene cada uno de ellos. El listado deberá mostrar también aquellos fabricantes que no tienen productos asociados.
```bash
SELECT f.nombre AS 'nombre de fabricante', p.nombre, f.codigo
FROM fabricante f 
LEFT JOIN producto p ON (f.codigo = p.codigo_fabricante);
```

### 2. Devuelve un listado donde sólo aparezcan aquellos fabricantes que no tienen ningún producto asociado.
```bash
SELECT f.nombre AS 'nombre de fabricante', p.nombre, f.codigo
FROM producto p
RIGHT JOIN fabricante f   ON (f.codigo = p.codigo_fabricante)
WHERE p.nombre IS NULL;;
```

### 3. ¿Pueden existir productos que no estén relacionados con un fabricante? Justifique su respuesta.
```bash
No, porque la tabla producto tiene una clave foránea que la relaciona con la tabla fabricante y ésta es obligatoria.
```

### Consultas resumen

### 1. Calcula el número total de productos que hay en la tabla productos.
```bash
SELECT count(*) FROM producto;
```

### 2. Calcula el número total de fabricantes que hay en la tabla fabricante.
```bash
SELECT count(*) FROM fabricante;
```

### 3. Calcula el número de valores distintos de código de fabricante aparecen en la tabla productos.
```bash
SELECT count(DISTINCT codigo_fabricante) FROM producto;
```

### 4. Calcula la media del precio de todos los productos.
```bash
SELECT AVG(precio) FROM producto;
```

### 5. Calcula el precio más barato de todos los productos.
```bash
SELECT MIN(precio) FROM producto;
```

### 6. Calcula el precio más caro de todos los productos.
```bash
SELECT MAX(precio) FROM producto;
```

### 7. Lista el nombre y el precio del producto más barato.
```bash
SELECT nombre, precio FROM producto ORDER BY precio ASC LIMIT 1;
```

### 8. Lista el nombre y el precio del producto más caro.
```bash
SELECT nombre, precio FROM producto ORDER BY precio DESC LIMIT 1;
```

### 9. Calcula la suma de los precios de todos los productos.
```bash
SELECT SUM(precio) FROM producto;
```

### 10. Calcula el número de productos que tiene el fabricante Asus.
```bash
SELECT COUNT(*) 
FROM producto p
JOIN fabricante f ON (p.codigo_fabricante = f.codigo)
WHERE f.nombre = 'Asus';
```

### 11. Calcula la media del precio de todos los productos del fabricante Asus.
```bash
SELECT AVG(precio) 
FROM producto p
JOIN fabricante f ON (p.codigo_fabricante = f.codigo)
WHERE f.nombre = 'Asus';
```

### 12. Calcula el precio más barato de todos los productos del fabricante Asus.
```bash
SELECT MIN(precio) 
FROM producto p
JOIN fabricante f ON (p.codigo_fabricante = f.codigo)
WHERE f.nombre = 'Asus';
```

### 13. Calcula el precio más caro de todos los productos del fabricante Asus.
```bash
SELECT MIN(precio) 
FROM producto p
JOIN fabricante f ON (p.codigo_fabricante = f.codigo)
WHERE f.nombre = 'Asus';
```

### 14. Calcula la suma de todos los productos del fabricante Asus.
```bash
SELECT SUM(precio) 
FROM producto p
JOIN fabricante f ON (p.codigo_fabricante = f.codigo)
WHERE f.nombre = 'Asus';
```

### 15. Muestra el precio máximo, precio mínimo, precio medio y el número total de productos que tiene el fabricante Crucial.
```bash
SELECT MAX(precio), MIN(precio), AVG(precio), count(*)
FROM producto p
JOIN fabricante f ON (p.codigo_fabricante = f.codigo)
WHERE f.nombre = 'Crucial';
```

### 16. Muestra el número total de productos que tiene cada uno de los fabricantes. El listado también debe incluir los fabricantes que no tienen ningún producto. El resultado mostrará dos columnas, una con el nombre del fabricante y otra con el número de productos que tiene. Ordene el resultado descendentemente por el número de productos.
```bash
SELECT count(p.nombre), f.nombre
FROM producto p 
RIGHT JOIN fabricante f  ON (p.codigo_fabricante = f.codigo)
GROUP BY f.nombre
ORDER BY count(p.nombre) DESC;
```

### 17. Muestra el precio máximo, precio mínimo y precio medio de los productos de cada uno de los fabricantes. El resultado mostrará el nombre del fabricante junto con los datos que se solicitan.
```bash
SELECT MAX(p.precio), MIN(p.precio), AVG(p.precio), f.nombre
FROM producto p 
RIGHT JOIN fabricante f  ON (p.codigo_fabricante = f.codigo)
GROUP BY f.nombre;
```
