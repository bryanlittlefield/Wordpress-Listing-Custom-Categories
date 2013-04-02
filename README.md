Wordpress: Listing Custom Taxonomies Attached to a Custom Post Type
===================================



####List Out Categories and Children
```php
<?php
$taxonomyName = "yourCustomTaxonomyName";
$terms = get_terms($taxonomyName,array('parent' => 0));
foreach($terms as $term): ?>
    <ul>
      <h2><a href="<?php echo get_term_link($term->slug,$taxonomyName);?>"><?php echo $term->name;?></a></h2>
    <?php $term_children = get_term_children($term->term_id,$taxonomyName);
    foreach($term_children as $term_child_id): ?>
        <?php $term_child = get_term_by('id',$term_child_id,$taxonomyName); ?>
        <li><a href="#<?php echo strtolower($term_child->name); ?>"><?php echo $term_child->name; ?></a></li>
    <?php endforeach; ?>
    </ul>
<?php endforeach; ?>
```

####List Out Categories and Children and Post Within
```php
<div>
<?php
$taxonomyName = "yourCustomTaxonomyName";
$terms = get_terms($taxonomyName,array('parent' => 0));
foreach($terms as $term): ?>
    <ul>
      <h2><a href="<?php echo get_term_link($term->slug,$taxonomyName);?>"><?php echo $term->name;?></a></h2>
    <?php $term_children = get_term_children($term->term_id,$taxonomyName);
    foreach($term_children as $term_child_id): ?>
        <?php $term_child = get_term_by('id',$term_child_id,$taxonomyName); ?>
        <li><a href="#<?php echo strtolower($term_child->name); ?>"><?php echo $term_child->name; ?></a></li>
  		<ul>
			<?php $child_name =  $term_child->name;?>
			<?php
			$args=array(
			  'fruit' => $child_name,
			  'post_type' => 'service_areas',
			  'post_status' => 'publish',
			  'posts_per_page' => 5,
			  'caller_get_posts'=> 1
			);
	        $my_query = null;
	        $my_query = new WP_Query($args);?>
				<?php while ( $my_query->have_posts() ) : $my_query->the_post(); ?>
				<li> <a href="<?php the_permalink(); ?>"><?php the_title(); ?></a></li>
				 <?php endwhile; ?>
			</ul>
        </li>
    <?php endforeach; ?>
    </ul>
<?php endforeach; ?>
</div>
```
