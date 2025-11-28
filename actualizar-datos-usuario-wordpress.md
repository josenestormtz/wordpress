# 🧩 Cómo actualizar datos de un usuario en WordPress y WooCommerce utilizando PHP

En WordPress es posible actualizar la información de cualquier usuario directamente desde PHP, incluyendo los datos nativos del usuario (nombre, apellido, correo) así como los campos de facturación y envío que utiliza WooCommerce.

Este tutorial explica cómo hacerlo de forma segura y sencilla.

✅ 1. Actualizar datos básicos del usuario (WordPress)

WordPress permite actualizar los campos principales de un usuario usando la función wp_update_user().
Los campos más comunes son:

Nombre (first_name)

Apellido (last_name)

Correo electrónico (user_email)

Ejemplo:
$user_id = 123; // ID del usuario

wp_update_user([
    'ID'         => $user_id,
    'first_name' => 'Néstor',
    'last_name'  => 'Gómez',
    'user_email' => 'correo@dominio.com'
]);

✅ 2. Actualizar datos de facturación y envío (WooCommerce)

WooCommerce almacena la información del cliente como user meta, lo que significa que podemos modificarla usando update_user_meta().

Campos de facturación más importantes:
Campo	Meta Key
Nombre	billing_first_name
Apellido	billing_last_name
Dirección	billing_address_1
Ciudad	billing_city
Estado/Provincia	billing_state
Código Postal	billing_postcode
País	billing_country
Teléfono	billing_phone

Los campos de envío utilizan la misma estructura, pero comienzan con shipping_.

✅ Ejemplo completo: actualizar todos los campos
$user_id = 123;

// === WordPress ===
wp_update_user([
    'ID'         => $user_id,
    'first_name' => 'Néstor',
    'last_name'  => 'Gómez',
    'user_email' => 'correo@dominio.com'
]);

// === WooCommerce Billing ===
update_user_meta($user_id, 'billing_first_name', 'Néstor');
update_user_meta($user_id, 'billing_last_name', 'Gómez');
update_user_meta($user_id, 'billing_address_1', 'Calle 123');
update_user_meta($user_id, 'billing_city', 'Ciudad de México');
update_user_meta($user_id, 'billing_state', 'CMX');
update_user_meta($user_id, 'billing_postcode', '01000');
update_user_meta($user_id, 'billing_country', 'MX');
update_user_meta($user_id, 'billing_phone', '5512345678');

// === WooCommerce Shipping ==== (Opcional)
update_user_meta($user_id, 'shipping_first_name', 'Néstor');
update_user_meta($user_id, 'shipping_last_name', 'Gómez');
update_user_meta($user_id, 'shipping_address_1', 'Calle 123');
update_user_meta($user_id, 'shipping_city', 'Ciudad de México');
update_user_meta($user_id, 'shipping_state', 'CMX');
update_user_meta($user_id, 'shipping_postcode', '01000');
update_user_meta($user_id, 'shipping_country', 'MX');

⚠️ Nota importante sobre códigos de país y estado

WooCommerce requiere códigos oficiales:

País → ISO 2 (México = MX, España = ES)

Estados → códigos compatibles (CMX, JAL, NLE, etc.)

Si los códigos no son correctos, los campos podrían no guardarse correctamente.

🎉 Listo

Con este método puedes actualizar cualquier información del usuario desde un snippet, plugin propio o integración externa.
