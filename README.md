Multi level category multiselect CodeIgniter
==========
related this topic:

 * generate data for Multi level category or menu in multiselect of CodeIgniter
 * A recursive method to storing hierarchical data without multiple calls to the database
 * Infinite dynamic Multi-level nested category with Codeigniter and MySQL
 * Get all categories (multilevel) A category can have many subcategories and a subcategory can have many sub-sub categories.
 

How To Use?

1.copy ```control_general.php``` file to library folder.
```
application/library
```
2.load library.
```
$this->load->library ( 'control_general' );
```

3.set initial values

my sample table is
```
| id | parent_id |  name   |
|----|-----------|---------|
| 10 |      0    | 'menu1' |
| 12 |     10    | 'menu2' |
| 13 |     10    | 'menu3' |
| 14 |      0    | 'menu4' |
```
<br/>
initial parms is
```
  $params = array (   
 'menu_id' => 'id',        
 'menu_title' => 'name',        
 'menu_parent' => 'parent_id',        
 'menu_parent_default_value' => '0',        
 'space_character' => " -> "        
 );
```

		$this->control_general->initialize($params);

4.generate data from table

 ```
 $list_build=$ci->control_general->generate_list($menu_list_from_table);
 ```
  
  Generated List Is 
```
 [1] => Array ( [107] => تست1 ) 
 [2] => Array ( [111] => تست 4 )
 [3] => Array ( [109] => -> تست 1 ) 
 [4] => Array ( [115] => -> تست7 ) 
 [5] => Array ( [110] => -> -> تست 3 ) 
 [6] => Array ( [112] => -> تست 4 ) 
 [7] => Array ( [113] => -> تست 5 )
 [8] => Array ( [114] => -> تست شش6 )
 [9] => Array ( [108] => -> -> تست 2 )
```
5.inject data genarated to ```$form->multi_select()```
 
 ```
    echo(form_multiselect (
    'menulist[]',
    $list_build,
    $menu_selected_list ,
    array("class"=>"form-control")  )
		);
```    
or built multi select by 

```$this->control_general->generate_multi_select($name, $list_build, $selected_list, $extra)```
