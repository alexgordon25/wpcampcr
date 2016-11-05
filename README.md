# Creando Temas Personalizados para Clientes.

## Presentación.

- [Creando-Temas-Personalizados-para-Clientes.WCCR2016.pdf](https://github.com/alexgordon25/wpcampcr/blob/master/presentacion/Creando-Temas-Personalizados-para-Clientes.WCCR2016.pdf)

## Caso de Ejemplo.

El Cliente requiere un sitio web con una sección principal de catálogo de Películas y otra de Noticias, el resto de paginas del sitio son estáticas.

PORTADA
	- PELICULAS
	- NOTICIAS
	- ACERCA DE NOSOTROS
	- CONTACTENOS

### Herramientas utilizadas.
- [Tema base de Underscores](http://underscores.me/)
- [WP Generate](https://generatewp.com/)
- [Advanced Custom Fields](https://www.advancedcustomfields.com/)

### Registro de "Custom Post Type" Película.

Agregar al final de function.php

```php
function register_movie_post_type() {

	$labels = array(
		'name'                  => _x( 'Películas', 'Post Type General Name', 'wpcampcr' ),
		'singular_name'         => _x( 'Película', 'Post Type Singular Name', 'wpcampcr' ),
		'menu_name'             => __( 'Películas', 'wpcampcr' ),
		'name_admin_bar'        => __( 'Película', 'wpcampcr' ),
		'archives'              => __( 'Item Archives', 'wpcampcr' ),
		'parent_item_colon'     => __( 'Parent Item:', 'wpcampcr' ),
		'all_items'             => __( 'All Items', 'wpcampcr' ),
		'add_new_item'          => __( 'Agregar Nueva Película', 'wpcampcr' ),
		'add_new'               => __( 'Agregar Película', 'wpcampcr' ),
		'new_item'              => __( 'Nueva Película', 'wpcampcr' ),
		'edit_item'             => __( 'Editar Película', 'wpcampcr' ),
		'update_item'           => __( 'Actualizar Película', 'wpcampcr' ),
		'view_item'             => __( 'Ver Película', 'wpcampcr' ),
		'search_items'          => __( 'Search Item', 'wpcampcr' ),
		'not_found'             => __( 'Not found', 'wpcampcr' ),
		'not_found_in_trash'    => __( 'Not found in Trash', 'wpcampcr' ),
		'featured_image'        => __( 'Featured Image', 'wpcampcr' ),
		'set_featured_image'    => __( 'Set featured image', 'wpcampcr' ),
		'remove_featured_image' => __( 'Remove featured image', 'wpcampcr' ),
		'use_featured_image'    => __( 'Use as featured image', 'wpcampcr' ),
		'insert_into_item'      => __( 'Insert into item', 'wpcampcr' ),
		'uploaded_to_this_item' => __( 'Uploaded to this item', 'wpcampcr' ),
		'items_list'            => __( 'Items list', 'wpcampcr' ),
		'items_list_navigation' => __( 'Items list navigation', 'wpcampcr' ),
		'filter_items_list'     => __( 'Filter items list', 'wpcampcr' ),
	);
	$rewrite = array(
		'slug'                  => 'pelicula',
		'with_front'            => true,
		'pages'                 => true,
		'feeds'                 => true,
	);
	$args = array(
		'label'                 => __( 'Película', 'wpcampcr' ),
		'description'           => __( 'Películas para wpcampcr', 'wpcampcr' ),
		'labels'                => $labels,
		'supports'              => array( 'title', 'editor', ),
		'hierarchical'          => false,
		'public'                => true,
		'show_ui'               => true,
		'show_in_menu'          => true,
		'menu_position'         => 5,
		'menu_icon'             => 'dashicons-format-video',
		'show_in_admin_bar'     => true,
		'show_in_nav_menus'     => true,
		'can_export'            => true,
		'has_archive'           => true,		
		'exclude_from_search'   => false,
		'publicly_queryable'    => true,
		'rewrite'               => $rewrite,
		'capability_type'       => 'page',
	);
	register_post_type( 'movie', $args );

}
add_action( 'init', 'register_movie_post_type', 0 );
```

### Registro de "Custom Taxonomy" Género

Agregar al final de function.php

```php
function register_genre_taxonomy() {

	$labels = array(
		'name'                       => _x( 'Géneros', 'Taxonomy General Name', 'wpcampcr' ),
		'singular_name'              => _x( 'Género', 'Taxonomy Singular Name', 'wpcampcr' ),
		'menu_name'                  => __( 'Géneros', 'wpcampcr' ),
		'all_items'                  => __( 'All Items', 'wpcampcr' ),
		'parent_item'                => __( 'Parent Item', 'wpcampcr' ),
		'parent_item_colon'          => __( 'Parent Item:', 'wpcampcr' ),
		'new_item_name'              => __( 'Agregar Género', 'wpcampcr' ),
		'add_new_item'               => __( 'Agregar Nuevo Género', 'wpcampcr' ),
		'edit_item'                  => __( 'Editar Género', 'wpcampcr' ),
		'update_item'                => __( 'Actualizar Género', 'wpcampcr' ),
		'view_item'                  => __( 'Ver Género', 'wpcampcr' ),
		'separate_items_with_commas' => __( 'Separate items with commas', 'wpcampcr' ),
		'add_or_remove_items'        => __( 'Add or remove items', 'wpcampcr' ),
		'choose_from_most_used'      => __( 'Choose from the most used', 'wpcampcr' ),
		'popular_items'              => __( 'Popular Items', 'wpcampcr' ),
		'search_items'               => __( 'Search Items', 'wpcampcr' ),
		'not_found'                  => __( 'Not Found', 'wpcampcr' ),
		'no_terms'                   => __( 'No items', 'wpcampcr' ),
		'items_list'                 => __( 'Items list', 'wpcampcr' ),
		'items_list_navigation'      => __( 'Items list navigation', 'wpcampcr' ),
	);
	$rewrite = array(
		'slug'                       => 'genero',
		'with_front'                 => true,
		'hierarchical'               => false,
	);
	$args = array(
		'labels'                     => $labels,
		'hierarchical'               => false,
		'public'                     => true,
		'show_ui'                    => true,
		'show_admin_column'          => true,
		'show_in_nav_menus'          => true,
		'show_tagcloud'              => true,
		'rewrite'                    => $rewrite,
	);
	register_taxonomy( 'genre', array( 'movie' ), $args );

}
add_action( 'init', 'register_genre_taxonomy', 0 );
```
