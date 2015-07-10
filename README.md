# laravel5 - Cache&Pagination
Laravel 5 ile sayfalama ve cache özelliği bir arada kullanımı

## her sayfayı ayrı ayrı cacheleyecektir.

$perCount = '10'; // Sayfa başına gösterilecek veri

//page değerini alıyoruz eğer yoksa 1 olarak set ediyoruz.

        if(Request::get('page'))
        {
            $pagenumber = Request::get('page');
        }
        else
        {
            $pagenumber = 1;
        }

        if(!Cache::has('pagination-'.$pagenumber)) Cache::add('pagination-'.$pagenumber,Blog::paginate($perCount),60);
        
        //Cache den veriyi alıyoruz.
        
        $samePost = Cache::get('pagination-'.$pagenumber);


        return view('blog.blog-list', ['data' => $samePost, 'pagination' => $samePost]);
        

### view de kullanımı
  
  // Örnek kullanım
  
  @foreach ($data as $post)
    
    {{  $post->id }}
    {{  $post->title  }}
  
  @endforeach


 <!-- pagination-->
        {!! str_replace('/?', '?', $pagination->render()) !!}
