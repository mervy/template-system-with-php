# Template System With PHP

- A ideia é não usar tags PHP nas páginas html mas ter as funcionalidades de laços
for, foreach, usar if, else entre outros mesmo sem usar as tags php

- Usar sistemas prontos e tentar adaptar os que existem para um template "homemade"

## Template System
### 1. Mustache
- https://mustache.github.io/
- https://www.carlosgonzalezgurrea.es/generando-paginas-con-el-sistema-de-plantillas-mustache/
- https://www.youtube.com/watch?v=B7hIR_Ii_d4 
- https://dev.to/thedevdrawer/creating-a-single-page-application-using-mustache-and-php-38ej 

```html
<h1>{{header}}</h1>
{{#bug}}
{{/bug}}

{{#items}}
  {{#first}}
    <li><strong>{{name}}</strong></li>
  {{/first}}
  {{#link}}
    <li><a href="{{url}}">{{name}}</a></li>
  {{/link}}
{{/items}}

{{#empty}}
  <p>The list is empty.</p>
{{/empty}}

```

### 2. Volt: Template Engine
- https://docs.phalcon.io/3.4/en/volt.html

```
{# app/views/products/show.volt #}

{% block last_products %}

{% for product in products %}
    * Name: {{ product.name|e }}
    {% if product.status === 'Active' %}
       Price: {{ product.price + product.taxes/100 }}
    {% endif  %}
{% endfor  %}

{% endblock %}
```

### 3. Plates 
- https://platesphp.com/

Controller:
```php
// Create new Plates instance
$templates = new League\Plates\Engine('/path/to/templates');

// Render a template
echo $templates->render('profile', ['name' => 'Jonathan']);
```

profile.php:
```php
<?php $this->layout('template', ['title' => 'User Profile']) ?>

<h1>User Profile</h1>
<p>Hello, <?=$this->e($name)?></p>
```

template.php:
```php
<html>
  <head>
    <title><?=$this->e($title)?></title>
  </head>
  <body>
    <?=$this->section('content')?>
  </body>
</html>
```

### 4. Blade 
- https://laravel.com/docs/10.x/blade#html-entity-encoding

```php
@if (count($records) === 1)
    I have one record!
@elseif (count($records) > 1)
    I have multiple records!
@else
    I don't have any records!
@endif
```

```php
@hasSection('navigation')
    <div class="pull-right">
        @yield('navigation')
    </div>
 
    <div class="clearfix"></div>
@endif
```

### 5. Smart 
- https://www.smarty.net/

```php
<h1>{$title|escape}</h1>
<ul>
    {foreach $cities as $city}
        <li>{$city.name|escape} ({$city.population})</li>
    {foreachelse}
        <li>no cities found</li>        
    {/foreach}
</ul>
```
https://github.com/smarty-php/smarty/blob/v4.3.2/docs/getting-started.md

### 6. Latte 
- https://latte.nette.org/en/
 
 ```php
 <ul>
    {foreach $users as $user}
        <li>{$user->name}</li>
    {/foreach}
</ul>

```php
{if $post->status === Status::Published}
    Read post
{elseif count($posts) > 0}
    See other posts
{/if}
```

```php
{$product?->getDiscount()}

{$foo[0] + strlen($bar[Bar::Const])}

{array_filter($nums, fn($n) => $n < 100)}
```

```php
<ul n:if="count($menu) > 1" class="menu">
    <li n:foreach="$menu as $item">
        <a n:tag-if="$item->href" href="{$item->href}">
            {$item->caption}
        </a>
    </li>
</ul>
```

