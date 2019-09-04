# If-need-to-fixed-post-within-a-row-in-post-query








//start <tr> 
if ( $query->have_posts() ) {
$i = 0;
                while ( $query->have_posts() ) {
 
// If $i is 5 (5th post), end one row and start the next
if (++$i == 5) {
echo '</tr><tr>';
}
// the rest of your loop output
//end </tr>









OR


$i = 1;
//added before to ensure it gets opened
echo '<div>';
if ( $wp_query->have_posts() ) : while ( $wp_query->have_posts() ) : $wp_query->the_post();
     // post stuff...
 
     // if multiple of 3 close div and open a new div
     if($i % 3 == 0) {echo '</div><div>';}
 
$i++; endwhile; endif;
//make sure open div is closed
echo '</div>';





In shortcode:



function testimonial_thumb_shortcode($atts){
    extract(shortcode_atts(array(
        'category' => ''
    ), $atts));
    $q = new WP_Query(array(
        'posts_per_page' => -1,
        'post_type' => 'testimonials',
        'testimonial_cat' => $category
    ));
    $list = ' <ul><li>';
 
    $i = 0; //init the counter
 
    while($q->have_posts()):
        $q->the_post();
        $idd = get_the_ID();
        $author_photo = wp_get_attachment_image_src(get_post_thumbnail_id($post->ID), 'thumbnail');
        $list .= '/*Main loop*/';
 
        $i++; //increase counter
        if($i % 2 == 0){
            $list .= '</li><li>';
        }
 
    endwhile;
    $list.= '</li></ul>';
    wp_reset_query();
    return $list;
}
add_shortcode('tthumb', 'testimonial_thumb_shortcode');
