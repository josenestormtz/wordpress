# Integrar SweetAlert2 en WordPress

## 💡 Objetivo
Integrar **SweetAlert2** (la versión moderna) en una página o en todo tu sitio WordPress sin romper dependencias ni editar archivos del tema.

## 🚀 Método recomendado: ```usando wp_enqueue_script```
Esta es la **forma más segura y profesional**, ya que usa el sistema nativo de WordPress para cargar scripts y evita conflictos con minificadores, caché o constructores.

## 🔧 Paso 1: Agrega este snippet
Ve a tu plugin **Code Snippets** (o ```functions.php``` si prefieres) y agrega lo siguiente:

```php
function integrar_sweetalert_en_wp() {
    // Registrar SweetAlert2 desde CDN
    wp_register_script(
        'sweetalert2',
        'https://cdn.jsdelivr.net/npm/sweetalert2@11',
        array('jquery'),
        null,
        true // cargar al final del body
    );

    // Encolar el script
    wp_enqueue_script('sweetalert2');

    // Opcional: agrega un script propio para usar SweetAlert
    wp_add_inline_script('sweetalert2', "
        document.addEventListener('DOMContentLoaded', function() {
            console.log('✅ SweetAlert2 cargado correctamente');
            // Ejemplo de alerta
            // Swal.fire('¡Hola, Néstor!', 'SweetAlert2 está funcionando 🎉', 'success');
        });
    ");
}
add_action('wp_enqueue_scripts', 'integrar_sweetalert_en_wp');
```

## 🧱 Paso 2: Verifica la carga
1. Abre tu sitio.
2. Presiona **F12 → Consola**.
Verás el mensaje ✅ “**SweetAlert2 cargado correctamente**”.
3. Si descomentas la línea del ejemplo, verás la alerta visual al cargar la página.

## 🎯 Opcional: Cargar solo en una página específica
Para no afectar todo el sitio, puedes limitarlo, por ejemplo, a la página del carrito o checkout:
```php
if ( is_page('carrito') ) {
    wp_enqueue_script('sweetalert2');
}
```
O por ID:
```php
if ( is_page(123) ) { ... }
```

## 🎨 Paso 3 (opcional): Agregar CSS personalizado
SweetAlert2 incluye su propio estilo, pero puedes modificarlo agregando en **CSS adicional**:
```css
.swal2-popup {
    font-family: 'Poppins', sans-serif;
    border-radius: 12px;
}
```

## ✅ Resultado

Con este método, SweetAlert se integrará correctamente sin modificar archivos del tema ni afectar otros scripts.

Listo para usar con cualquier llamada de JavaScript o jQuery, por ejemplo:
```js
Swal.fire({
  title: '¡Listo!',
  text: 'Tu pedido fue enviado correctamente.',
  icon: 'success'
});
```
