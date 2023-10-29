# Disenio-de-Base-de-Datos
CREATE DATABASE BetterOption;
CREATE TABLE usuario (
 usuarioID int primary key not null,
 nombre varchar(50),
 apellido varchar(20),
 tipo varchar(30),
 correo_electrónico varchar(50),
 contrasenia varchar(13),
 dni varchar(40),
 numero_tarjeta int,
 telefono char(9),
);
go 

CREATE TABLE compra(
  compraID int primary Key not null,
  fecha_compra datetime,
  compras_realizadas int,
  id_usuario int FOREIGN KEY references usuario(usuarioID)
);
go 

CREATE TABLE pago(
  pagoID int primary Key not null,
  id_compra int FOREIGN KEY references compra(compraID),
  tipo_pago varchar(100),
  monto money
);
go

CREATE TABLE suscripcion ( 
  suscripcionID int primary Key not null,
  id_usuario int FOREIGN KEY references usuario(usuarioID),
  tipo_suscripcion varchar(100),
  fecha_inicio datetime,
  fecha_final datetime,
  beneficio text,
);
go

CREATE TABLE producto(
  productoID int primary Key not null,
  nombre varchar(100),
  descripcion varchar(400),
  categoria varchar(100),
  precio money,
  stock int
);
go

CREATE TABLE tienda (
  tiendaID int primary key not null,
  nombre varchar(100),
  direccion varchar(100),
  tipo_tienda varchar(100),
);
go

CREATE TABLE anuncio (
  anuncioID int primary key not null,
  contenido text,
  fecha datetime,
  id_tienda int FOREIGN KEY references tienda(tiendaID),
);
go

CREATE TABLE descuento ( 
  ofertaID int primary key not null,
  descuento float(3),
  fecha_inicio datetime,
  fecha_final datetime,
  id_producto int FOREIGN KEY references producto(productoID),
  );
  go

CREATE TABLE detalle_compra(
  detalle_compraID int PRIMARY KEY not null,
  cantidad int,
  id_compra int FOREIGN KEY references compra(compraID),
  id_producto int FOREIGN KEY references producto(productoID)
);
go

CREATE TABLE busqueda(
  fecha_busqueda datetime PRIMARY KEY not null,
  id_usuario int FOREIGN key references usuario(usuarioID),
  id_producto int FOREIGN key references producto(productoID)
);
go

CREATE TABLE producto_tienda(
  id_tienda int primary KEY FOREIGN key references tienda(tiendaID),
  id_producto int FOREIGN key references producto(productoID)
);
go

CREATE TABLE producto_anuncio(
  id_producto int PRIMARY KEY FOREIGN key references producto(productoID),
  id_anuncio int FOREIGN key references anuncio(anuncioID)
);
