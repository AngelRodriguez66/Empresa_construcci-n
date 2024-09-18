# Empresa_construcción

<details>
<summary><h2>1. Creación de la estrutura de la base de datos SQL (Tablas y Relaciones). </h2></summary>
    
```sql
-- Crear la base de datos
CREATE DATABASE EmpresaConstruccion;
USE EmpresaConstruccion;

-- Tabla de empleados
CREATE TABLE Empleados (
    empleado_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre VARCHAR(50),
    apellido VARCHAR(50),
    email VARCHAR(100),
    telefono VARCHAR(20),
    puesto_id INT,
    salario DECIMAL(10, 2),
    fecha_contratacion DATE,
    FOREIGN KEY (puesto_id) REFERENCES Puestos(puesto_id) -- Relación uno a muchos con Puestos
);

-- Tabla de puestos
CREATE TABLE Puestos (
    puesto_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre_puesto VARCHAR(50),
    descripcion TEXT
);

-- Tabla de proyectos
CREATE TABLE Proyectos (
    proyecto_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre_proyecto VARCHAR(100),
    cliente_id INT,
    fecha_inicio DATE,
    fecha_fin DATE,
    presupuesto DECIMAL(15, 2),
    FOREIGN KEY (cliente_id) REFERENCES Clientes(cliente_id) -- Relación uno a muchos con Clientes
);

-- Tabla de clientes
CREATE TABLE Clientes (
    cliente_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre_cliente VARCHAR(100),
    email_cliente VARCHAR(100),
    telefono_cliente VARCHAR(20)
);

-- Tabla de materiales
CREATE TABLE Materiales (
    material_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre_material VARCHAR(100),
    descripcion TEXT,
    precio_unitario DECIMAL(10, 2)
);

-- Tabla de proveedores
CREATE TABLE Proveedores (
    proveedor_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre_proveedor VARCHAR(100),
    email_proveedor VARCHAR(100),
    telefono_proveedor VARCHAR(20)
);

-- Relación muchos a muchos entre Materiales y Proveedores
CREATE TABLE ProveedorMaterial (
    proveedor_id INT,
    material_id INT,
    PRIMARY KEY (proveedor_id, material_id),
    FOREIGN KEY (proveedor_id) REFERENCES Proveedores(proveedor_id),
    FOREIGN KEY (material_id) REFERENCES Materiales(material_id)
);

-- Tabla de almacenes
CREATE TABLE Almacenes (
    almacen_id INT PRIMARY KEY AUTO_INCREMENT,
    ubicacion VARCHAR(100),
    capacidad INT
);

-- Tabla de materiales en almacén (uno a muchos)
CREATE TABLE MaterialesAlmacen (
    almacen_id INT,
    material_id INT,
    cantidad INT,
    PRIMARY KEY (almacen_id, material_id),
    FOREIGN KEY (almacen_id) REFERENCES Almacenes(almacen_id),
    FOREIGN KEY (material_id) REFERENCES Materiales(material_id)
);

-- Tabla de departamentos de la empresa
CREATE TABLE Departamentos (
    departamento_id INT PRIMARY KEY AUTO_INCREMENT,
    nombre_departamento VARCHAR(50),
    presupuesto_anual DECIMAL(15, 2)
);

-- Relación uno a muchos entre Empleados y Departamentos
ALTER TABLE Empleados ADD COLUMN departamento_id INT;
ALTER TABLE Empleados ADD FOREIGN KEY (departamento_id) REFERENCES Departamentos(departamento_id);

-- Relación uno a uno entre empleados y usuarios de sistema
CREATE TABLE UsuariosSistema (
    usuario_id INT PRIMARY KEY AUTO_INCREMENT,
    empleado_id INT,
    username VARCHAR(50),
    password VARCHAR(100),
    rol VARCHAR(20),
    FOREIGN KEY (empleado_id) REFERENCES Empleados(empleado_id) -- Relación uno a uno con empleados
);

```
</details>

<details>
<summary><h2>2. Inserción de los datos en la base de datos creada.</h2></summary>
    

```sql
-- Insertar datos en la tabla Puestos
INSERT INTO Puestos (nombre_puesto, descripcion) VALUES 
('Ingeniero Civil', 'Responsable de la planificación y ejecución de proyectos'),
('Administrador', 'Encargado de la gestión administrativa'),
('Albañil', 'Realiza labores de construcción en el campo');

-- Insertar datos en la tabla Departamentos
INSERT INTO Departamentos (nombre_departamento, presupuesto_anual) VALUES
('Construcción', 500000.00),
('Administración', 200000.00),
('Logística', 150000.00);

-- Insertar datos en la tabla Empleados
INSERT INTO Empleados (nombre, apellido, email, telefono, puesto_id, salario, fecha_contratacion, departamento_id) VALUES 
('Juan', 'Pérez', 'juan.perez@empresa.com', '123456789', 1, 3500.00, '2022-05-01', 1),
('Ana', 'García', 'ana.garcia@empresa.com', '987654321', 2, 4000.00, '2021-08-15', 2),
('Carlos', 'Martínez', 'carlos.martinez@empresa.com', '555555555', 3, 2500.00, '2023-01-10', 1);

-- Insertar datos en la tabla Clientes
INSERT INTO Clientes (nombre_cliente, email_cliente, telefono_cliente) VALUES
('Constructora ABC', 'contacto@abc.com', '123123123'),
('Desarrolladora XYZ', 'info@xyz.com', '321321321');

-- Insertar datos en la tabla Proyectos
INSERT INTO Proyectos (nombre_proyecto, cliente_id, fecha_inicio, fecha_fin, presupuesto) VALUES
('Edificio Central', 1, '2023-06-01', '2024-06-01', 1200000.00),
('Parque Residencial', 2, '2022-03-15', '2023-09-20', 800000.00);

-- Insertar datos en la tabla Materiales
INSERT INTO Materiales (nombre_material, descripcion, precio_unitario) VALUES
('Cemento', 'Cemento de alta calidad', 50.00),
('Ladrillo', 'Ladrillo rojo estándar', 0.80),
('Varilla', 'Varilla de acero de 1 pulgada', 10.00);

-- Insertar datos en la tabla Proveedores
INSERT INTO Proveedores (nombre_proveedor, email_proveedor, telefono_proveedor) VALUES
('Proveedor A', 'contacto@proveedora.com', '111111111'),
('Proveedor B', 'ventas@proveedorb.com', '222222222');

-- Relacionar Materiales con Proveedores (muchos a muchos)
INSERT INTO ProveedorMaterial (proveedor_id, material_id) VALUES
(1, 1),
(1, 2),
(2, 3);

-- Insertar datos en la tabla Almacenes
INSERT INTO Almacenes (ubicacion, capacidad) VALUES
('Almacén Central', 1000),
('Almacén Secundario', 500);

-- Insertar datos en la tabla MaterialesAlmacen
INSERT INTO MaterialesAlmacen (almacen_id, material_id, cantidad) VALUES
(1, 1, 200),
(1, 2, 500),
(2, 3, 150);

```

</details>

<details>
<summary><h2>3. Creación del diagrama para la visualización efectiva de los datos.</h2></summary>
    

    3.1. Creación del diagrama con Workbench (Muy buena visualización).
        ![Captura desde 2024-09-18 15-48-05](https://github.com/user-attachments/assets/da7ec268-b2fa-4d74-bd13-340b696dd329)
        ![Captura desde 2024-09-18 15-49-32](https://github.com/user-attachments/assets/a871b2fa-0d46-4885-8d4a-072d86f01bf1)
        ![Captura desde 2024-09-18 15-52-44](https://github.com/user-attachments/assets/af888085-08c5-4e6b-81ff-d00473c211a5)
        ![Captura desde 2024-09-18 15-53-56](https://github.com/user-attachments/assets/c31faaf7-8f4e-4632-9a7f-6cc0011c641e)
        
    3.2. Creación del diagrama con DrawDB.
       3.2.1. Ir a Workbench y exportar la bse de datos en un archivo SQL.
       3.2.2. Ir a DrawDB, crear un archivo nuevo, 'Archivo', 'Importar desde fuente' y seleccionar el archivo. OJO!! revisar relaciones, pueden haber fallos.
        ![Captura desde 2024-09-18 16-07-43](https://github.com/user-attachments/assets/d549d346-0921-409c-b03f-1a1f505ee451)

</details>

<details>
<summary><h2>4. Redacción de querys básicas para el entendimiento de la sintaxis básica de SQL.</h2></summary>
    
 <details>
<summary>4.1. Seleccionar todos los empleados y su puesto.</summary>

```sql
SELECT E.nombre, E.apellido, P.nombre_puesto 
FROM Empleados E
JOIN Puestos P ON E.puesto_id = P.puesto_id;
```
</details>

   4.2. Filtrar empleados con salario mayor a 3000.

```sql
SELECT nombre, apellido, salario 
FROM Empleados 
WHERE salario > 3000;

```

   4.3. Ordenar proyectos por fecha de inicio.

```sql
SELECT nombre_proyecto, fecha_inicio 
FROM Proyectos 
ORDER BY fecha_inicio ASC;

```

   4.4. Limitar los resultados a los 3 primeros materiales más caros.

```sql
SELECT nombre_material, precio_unitario 
FROM Materiales 
ORDER BY precio_unitario DESC 
LIMIT 3;

```

   4.5. Contar el número de empleados en cada departamento.

```sql
SELECT D.nombre_departamento, COUNT(E.empleado_id) AS total_empleados
FROM Departamentos D
LEFT JOIN Empleados E ON D.departamento_id = E.departamento_id
GROUP BY D.nombre_departamento;

```

   4.6. Obtener la suma del presupuesto total de todos los proyectos.

```sql
SELECT SUM(presupuesto) AS presupuesto_total 
FROM Proyectos;

```

   4.7. Filtrar proveedores que suministran "Cemento".

```sql
SELECT P.nombre_proveedor 
FROM Proveedores P
JOIN ProveedorMaterial PM ON P.proveedor_id = PM.proveedor_id
JOIN Materiales M ON PM.material_id = M.material_id
WHERE M.nombre_material = 'Cemento';

```

   4.8. Actualizar el salario de un empleado

```sql
UPDATE Empleados 
SET salario = 4500.00 
WHERE empleado_id = 1;

```

   4.9. Eliminar un proyecto.

```sql
DELETE FROM Proyectos 
WHERE proyecto_id = 2;

```

   4.10. Agrupar los materiales por almacén y mostrar la cantidad total en cada uno

```sql
SELECT A.ubicacion, SUM(MA.cantidad) AS total_materiales
FROM Almacenes A
JOIN MaterialesAlmacen MA ON A.almacen_id = MA.almacen_id
GROUP BY A.ubicacion;
```

</details>

