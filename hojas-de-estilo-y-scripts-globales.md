# 🌐 Cómo agregar hojas de estilo y scripts JavaScript globales en WordPress

En WordPress, la forma correcta y recomendada de integrar archivos CSS o JavaScript que apliquen en todo el sitio es mediante la función **wp_enqueue_scripts**. Esto garantiza compatibilidad con WordPress, evita conflictos y permite controlar versiones y dependencias.

## 📁 1. Agregar una hoja de estilo global (CSS)
### Paso 1: Coloca tu archivo en el tema hijo
Guarda tu archivo aquí:
```swift
/wp-content/themes/tu-tema-hijo/css/custom.css
```

### Paso 2: Encola el CSS en functions.php
```php
function estilos_globales_personalizados() {
    wp_enqueue_style(
        'estilos-custom', 
        get_stylesheet_directory_uri() . '/css/custom.css',
        array(),
        '1.0'
    );
}
add_action('wp_enqueue_scripts', 'estilos_globales_personalizados');
```
- ✔ Este archivo se cargará en todo el sitio.
- ✔ No se pierde al actualizar el tema (porque está en el tema hijo).

## 📜 2. Agregar un archivo JavaScript global
### Paso 1: Guarda tu script aquí:
```swift
/wp-content/themes/tu-tema-hijo/js/custom.js
```

### Paso 2: Encola el JavaScript en functions.php
```php
function scripts_globales_personalizados() {
    wp_enqueue_script(
        'scripts-custom',
        get_stylesheet_directory_uri() . '/js/custom.js',
        array('jquery'), // dependencias opcionales
        '1.0',
        true // cargar en el footer
    );
}
add_action('wp_enqueue_scripts', 'scripts_globales_personalizados');
```
- ✔ `true` hace que cargue en el footer para mejor rendimiento.
- ✔ También se carga en **todo el sitio**.

## ➕ 3. Agregar código JS rápido usando inline script (opcional)
```php
add_action('wp_enqueue_scripts', function() {
    wp_add_inline_script('jquery', "
        console.log('Script global cargado');
    ");
});
```
Esto sirve para pequeños fragmentos sin necesidad de un archivo completo.

## 📌 Recomendaciones
- Usa **tema hijo (child theme)** para no perder cambios con actualizaciones.
- No insertes scripts directamente en plantillas usando `<script>` o `<style>`.
- Evita modificar el tema principal.
- Usa `CSS adicional` solo para ajustes rápidos, no para proyectos grandes.
