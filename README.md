# Hướng dẫn Export slug trong woocommerce (giaiphapmmo.net)
## Bước 1: Thêm đoạn code sau vào file wp-function.php
### Ảnh hướng dẫn sửa file function.php
![Alt text](https://github.com/ngochoaitn/export-slug-woocommerce/blob/main/Huong-dan-export-slug.png?raw=true)
### Đoạn code
```
// GPM Code export slug START
add_filter( 'woocommerce_product_export_column_names', 'add_slug_export_column' );
add_filter( 'woocommerce_product_export_product_default_columns', 'add_slug_export_column' );

function add_slug_export_column( $columns ) {
	$columns['slug'] = 'Slug';
 
	return $columns;
}

add_filter( 'woocommerce_product_export_product_column_slug'  , 'add_export_data_slug', 10, 2 );
function add_export_data_slug( $value, $product ) {
    $value = $product->get_slug();
	
    return $value;
}

add_filter( 'woocommerce_csv_product_import_mapping_options', 'add_slug_import_option' );
function add_slug_import_option( $options ) {
  $options['slug'] = 'Slug';
 
  return $options;
}

add_filter( 'woocommerce_csv_product_import_mapping_default_columns', 'add_default_slug_column_mapping' );
function add_default_slug_column_mapping( $columns ) {
  $columns['Slug'] = 'slug';
 
  return $columns;
} 

add_filter( 'woocommerce_product_import_pre_insert_product_object', 'process_import_product_slug_column', 10, 2 );
function process_import_product_slug_column( $object, $data ) {
  if ( !empty( $data['slug'] ) ) {
    $object->set_slug( $data['slug'] );
  }
 
  return $object;
}
// GPM Code export slug END
```
