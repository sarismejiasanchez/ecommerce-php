## Inicio

- Descarga o clona el repositorio e ingresa la carpeta ecommerce-php en la ubicación C:\laragon\www

- En la consola, dentro del directorio C:\laragon\www\ecommerce-php ingresar el siguiente codigo para instalar la librerias

```bash
#Actualizar librerias
composer update
```

## Configuración base de datos

- Ingresamos a la carpeta ecommerce-php ubicada en C:\laragon\www, realizamos un copia del archivo .env.example y la copia la nombramos .env

- Abrimos el proyecto desde Visual Studio Code e ingresamos al archivo .env para configurar la base de datos

- Creamos una base de datos desde el cliente que tengamos para realizar BD y de acuerdo a la configuración de la base de datos completamos la siguiente información en el archivo .env

```bash
DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=ecommerce-iud
DB_USERNAME=root
DB_PASSWORD=
```

- Nuevamente en la consola ingresamos el siguiente codigo

```bash
#Generar clave
php artisan key:generate
#Crear o Migrar las tablas en la base de datos
php artisan migrate
```

- En la base de datos se deben ejecutar los siguientes Scripts para poblar las tablas: 

```bash
insert into roles(id, name) values (1, 'ADMIN');
insert into roles(id, name) values (2, 'SELLER');

-- password por defecto para todos los usurios: 123456789
INSERT INTO users(id, role_id, seller_id, name, email, password, created_at, updated_at)
VALUES (1, 1, NULL, 'Admin', 'admin@admin.com', '$2y$10$ocpzmNFoHIwNWvY6H3ecue0QoWOOpNxHXZb3qlG6GM/MFXng7KWAi', NULL, NULL);

INSERT INTO categories(id, name) values (1, 'Calzado');
INSERT INTO categories(id, name) values (2, 'Tecnologia');
INSERT INTO categories(id, name) values (3, 'Cocina');
INSERT INTO categories(id, name) values (4, 'Celulares');
INSERT INTO categories(id, name) values (5, 'Construccion');
INSERT INTO categories(id, name) values (6, 'Belleza');
INSERT INTO categories(id, name) values (7, 'Deporte');
INSERT INTO categories(id, name) values (8, 'Accesorios');

INSERT INTO brands(id, name) values (1, 'Sony');
INSERT INTO brands(id, name) values (2, 'Apple');
INSERT INTO brands(id, name) values (3, 'HP');
INSERT INTO brands(id, name) values (4, 'Adidas');
INSERT INTO brands(id, name) values (5, 'Nike');
INSERT INTO brands(id, name) values (6, 'Samsung');
INSERT INTO brands(id, name) values (7, 'Trek');
INSERT INTO brands(id, name) values (8, 'Ray-Ban');

INSERT INTO `ecommerce-iud`.sellers (name,created_at,updated_at) VALUES
	 ('Tienda de bicicletas 4x4','2021-12-06 16:18:45','2021-12-06 16:18:45'),
	 ('Tienda de accesorios para salir','2021-12-06 16:18:59','2021-12-06 16:18:59');

INSERT INTO `ecommerce-iud`.users (name,email,email_verified_at,password,remember_token,role_id,seller_id,created_at,updated_at) VALUES
	 ('Adrian','adrian@gmail.com',NULL,'$2y$10$a9c41o1gcpHc4KpvyNF56O8qXyKzNC5KtYY/dmnxAtHDXxiJB.0LS',NULL,2,1,'2021-12-06 16:19:32','2021-12-06 16:19:32'),
	 ('Pedro','pedro@gmail.com',NULL,'$2y$10$dqMxtdLEtmRgwtLOw5M9le9A3EbPdsAUkpFc76Ipi4.ZhYnnvWyQ2',NULL,2,2,'2021-12-06 16:19:48','2021-12-06 16:19:48');

INSERT INTO `ecommerce-iud`.products (category_id,brand_id,name,description,image,price,inventory,seller_id,created_at,updated_at) VALUES
	 (7,7,'Bicicleta para montana','Color Negro','https://trek.scene7.com/is/image/TrekBicycleProducts/Supercaliber96_22_35151_A_Portrait?$responsive-pjpg$&cache=on,on&wid=1440&hei=1080',2000.0,500,1,'2021-12-06 16:26:31','2021-12-06 16:26:31'),
	 (8,8,'Gafas de Sol','AVIATOR CLASSIC
Lentes:  Verde Color liso  +  Montura:  Oro','https://images.ray-ban.com/is/image/RayBan/805289602057__STD__shad__qt.png?impolicy=RB_Product',145.0,30,2,'2021-12-06 16:40:46','2021-12-06 16:40:46'),
	 (2,2,'iPhone 13 Pro','Color: Sierra Blue
128 GB','https://store.storeimages.cdn-apple.com/4982/as-images.apple.com/is/iphone-13-pro-max-blue-select?wid=470&hei=556&fmt=png-alpha&.v=1631652955000',999.0,12,2,'2021-12-06 16:43:31','2021-12-06 16:43:31');

-- En la base de datos se corre el siguiente codigo para insertar datos de las categorias y las marcas:

INSERT INTO categories(id, name) values (1, 'Calzado');
INSERT INTO categories(id, name) values (2, 'Tecnología');
INSERT INTO categories(id, name) values (3, 'Cocina');
INSERT INTO categories(id, name) values (4, 'Celulares');
INSERT INTO categories(id, name) values (5, 'Construcción');
INSERT INTO categories(id, name) values (6, 'Belleza');
INSERT INTO categories(id, name) values (7, 'Deporte');
INSERT INTO categories(id, name) values (8, 'Accesorios');

INSERT INTO brands(id, name) values (1, 'Sony');
INSERT INTO brands(id, name) values (2, 'Apple');
INSERT INTO brands(id, name) values (3, 'HP');
INSERT INTO brands(id, name) values (4, 'Adidas');
INSERT INTO brands(id, name) values (5, 'Nike');
INSERT INTO brands(id, name) values (6, 'Samsung');
INSERT INTO brands(id, name) values (7, 'Trek');
INSERT INTO brands(id, name) values (8, 'Ray-Ban');
```

- Se ingresa a la aplicacion con el usuario y la contraseña del administrador

- La aplicación cuenta con las siguientes API las cuales pueden ser invocadas por https://www.postman.com/

Crear Productos, Listar Productos, Consultar Producto por Id

Crear Seller, Listar Sellers y Consultar Seller por Id

Crear Order y Consultar Order por Email

Para Crear Seller: http://ecommerce-php.test/api/seller

```bash
{
        "name": "Alkosto"
}
```

Para Crear Order se debe usar el siguiente JSON: http://ecommerce-php.test/api/order
```bash
{
    "email": "sara.mejia@est.iudigital.edu.co",
    "products": [
        {
            "id": 6,
            "quantity": 2
        },
        {
            "id": 5,
            "quantity": 1
        }
    ]
}
```

Para Consultar Seller por Id: http://ecommerce-php.test/api/seller/2

Para Consultar Order por Email: http://ecommerce-php.test/api/order/sara.mejia@est.iudigital.edu.co


<p align="center"><a href="https://laravel.com" target="_blank"><img src="https://raw.githubusercontent.com/laravel/art/master/logo-lockup/5%20SVG/2%20CMYK/1%20Full%20Color/laravel-logolockup-cmyk-red.svg" width="400"></a></p>

<p align="center">
<a href="https://travis-ci.org/laravel/framework"><img src="https://travis-ci.org/laravel/framework.svg" alt="Build Status"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/dt/laravel/framework" alt="Total Downloads"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/v/laravel/framework" alt="Latest Stable Version"></a>
<a href="https://packagist.org/packages/laravel/framework"><img src="https://img.shields.io/packagist/l/laravel/framework" alt="License"></a>
</p>

## About Laravel

Laravel is a web application framework with expressive, elegant syntax. We believe development must be an enjoyable and creative experience to be truly fulfilling. Laravel takes the pain out of development by easing common tasks used in many web projects, such as:

- [Simple, fast routing engine](https://laravel.com/docs/routing).
- [Powerful dependency injection container](https://laravel.com/docs/container).
- Multiple back-ends for [session](https://laravel.com/docs/session) and [cache](https://laravel.com/docs/cache) storage.
- Expressive, intuitive [database ORM](https://laravel.com/docs/eloquent).
- Database agnostic [schema migrations](https://laravel.com/docs/migrations).
- [Robust background job processing](https://laravel.com/docs/queues).
- [Real-time event broadcasting](https://laravel.com/docs/broadcasting).

Laravel is accessible, powerful, and provides tools required for large, robust applications.

## Learning Laravel

Laravel has the most extensive and thorough [documentation](https://laravel.com/docs) and video tutorial library of all modern web application frameworks, making it a breeze to get started with the framework.

If you don't feel like reading, [Laracasts](https://laracasts.com) can help. Laracasts contains over 1500 video tutorials on a range of topics including Laravel, modern PHP, unit testing, and JavaScript. Boost your skills by digging into our comprehensive video library.

## Laravel Sponsors

We would like to extend our thanks to the following sponsors for funding Laravel development. If you are interested in becoming a sponsor, please visit the Laravel [Patreon page](https://patreon.com/taylorotwell).

### Premium Partners

- **[Vehikl](https://vehikl.com/)**
- **[Tighten Co.](https://tighten.co)**
- **[Kirschbaum Development Group](https://kirschbaumdevelopment.com)**
- **[64 Robots](https://64robots.com)**
- **[Cubet Techno Labs](https://cubettech.com)**
- **[Cyber-Duck](https://cyber-duck.co.uk)**
- **[Many](https://www.many.co.uk)**
- **[Webdock, Fast VPS Hosting](https://www.webdock.io/en)**
- **[DevSquad](https://devsquad.com)**
- **[Curotec](https://www.curotec.com/services/technologies/laravel/)**
- **[OP.GG](https://op.gg)**
- **[CMS Max](https://www.cmsmax.com/)**
- **[WebReinvent](https://webreinvent.com/?utm_source=laravel&utm_medium=github&utm_campaign=patreon-sponsors)**

## Contributing

Thank you for considering contributing to the Laravel framework! The contribution guide can be found in the [Laravel documentation](https://laravel.com/docs/contributions).

## Code of Conduct

In order to ensure that the Laravel community is welcoming to all, please review and abide by the [Code of Conduct](https://laravel.com/docs/contributions#code-of-conduct).

## Security Vulnerabilities

If you discover a security vulnerability within Laravel, please send an e-mail to Taylor Otwell via [taylor@laravel.com](mailto:taylor@laravel.com). All security vulnerabilities will be promptly addressed.

## License

The Laravel framework is open-sourced software licensed under the [MIT license](https://opensource.org/licenses/MIT).
