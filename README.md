# Empresa_construcción
1. Creación del código SQL.
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
2. Creación del diagrama para la visualización efectiva de los datos.

