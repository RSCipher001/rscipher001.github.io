+++
categories = ["php", "laravel"]
date = "2021-04-04"
description = "Laravel snippets Cheatsheet"
title = "Laravel snippets Cheatsheet"
+++

### Controller Boilerplate
```php
//Project Controller

public function __construct()
{
    // Add middleware to all methods
    $this->middleware('active');

    // Add middleware to only specific methods
    $this->middleware('active')->only('index');

    // Add middleware to all methods except specific methods
    $this->middleware('active')->except('index');
}

public function index()
{
    // Get all projects for user->project relationship
    $projects = auth()->user()->project;
    return view('project.index', compact('projects'));

    // One liner
    return view('project.index')->with('projects', auth()->user()->project);
}

public function create()
{
    return view('project.create');
}

// NOTE: This is using ProjectRequest (Form Request) so data is already validated
public function store(ProjectRequest $request)
{
    // Save a model without relationship
    $project = new Project($request->validated());
    $project->save();

    // Save Project with user->project relationship
    auth()->user()->project()->save(new Project($request->validated()));
    return redirect('/project')->with('message', 'Project Added Successfully');

    // One-liner
    (new Project($request->validated()))->save();
}

public function show(Project $project)
{
    // Show Project
    return view('project.show', compact('project'));

    // Eager loading project->task relation
    $project->load('task');
    return view('project.show', compact('project'));

    // Send a 403
    abort(403);
}

public function edit(Project $project)
{
    return view('project.edit', compact('project'));
}

public function update(ProjectRequest $request, Project $project)
{
    $Project->update($request->validated());
    return redirect('/Project')->with('message', 'Project Updated Successfully');
    
}

public function destroy(Project $project)
{
    $address->delete();
    return redirect(route('project.index'))->with('message', 'Project Deleted Successfully');
}
```


### Form Request Boilerplate
```php

use Illuminate\Validation\Rule;

public function rules()
{
    return [
        'type' => ['required', Rule::in(['Home', 'Office'])],
        'city' => 'required|string|max:128',
        'state' => 'required|string|max:128',
        'pin' => 'required|digits:6'
    ];
}
```

### Multi File upload (Only Square Images)

```html
<!-- HTML Form -->
<input type="file" name="images[]" accept="image/*" multiple>
```

```php
// Form Request Class
public function rules()
{
    return [
        // dimensions:ratio=1/1 = Square, remove/change if neccessory
        'images.*' => 'bail|required|image|mimes:jpeg|dimensions:ratio=1/1',

        // Max 5 file uploads is allowed at once.
        'images' => 'max:5',
    ];
}

// Customized error messages
public function messages()
{
    return [
        'images.max' => 'Maximum 5 images are allowed at once.',
        'images.*.mimes' => 'Only jpeg images are allowed.',
        'images.*.dimensions' => 'Only square images are allowed.'
    ];
}
```

```php
// Controller, May need many changes
foreach ($request->images as $photo) {
    $path = $photo->storeAs('products', md5_file($photo) . '.jpg', 'public');
    try {
        $product->photo()->save(new Photo([
            'path' => $path,
        ]));
    } catch (Exception $exception) {
        continue;
    }
}
```

### Input YouTube Links
```php
// Validation Rules
public function rules()
{
  return [
      'link' => 'required|unique:product_videos,link',
  ];
}

// Extract ID from URL
protected function prepareForValidation()
{
  $this->merge([
      'link' => $this->extractYouTubeVideoId($this->link),
  ]);
}

// Custom Validation Messages
public function messages()
{
    return [
        'link.required' => 'Invalid link'
    ];
}

// Extract ID from URL
private function extractYouTubeVideoId($link)
{
    try {
        // For videos like http://www.youtube.com/watch?v=...
        $video_id = explode("?v=", $link);

        // For videos like http://www.youtube.com/watch/v/..
        if (empty($video_id[1])) {
            $video_id = explode("/v/", $link);
        }

        // Deleting any other params
        $video_id = explode("&", $video_id[1]);
        $video_id = $video_id[0];
        return $video_id;
    } catch (\Exception $exception) {
        return null;
    }
}
```


### CSV to Array
```html
<input class="form-control" name="value" type="text" required>
```

```php
public function rules()
{
    return [
        'tags' => 'required|array',
    ];
}

protected function prepareForValidation()
{
    $this->merge([
        'tags' => array_map(
            'ucfirst', array_map(
                'trim', explode(',', $this->value)
                )
            ),
    ]);
}
```

```php
// Controller
foreach ($request->tags as $value) {
    try {
        $product->attribute()->save(new ProductAttribute([
            'name' => $request->name,
            'value' => $value,
            'price' => $request->price,
        ]));
    } catch (Exception $exception) {
        continue;
    }
}
```

### Bootstrap Form Boilerplate
```html
<div class="form-group row">
    <label for="email" class="col-sm-4 col-form-label text-md-right">E-Mail Address</label>

    <div class="col-md-6">
        <input id="email" type="email" name="email" required autofocus
        class="form-control{% raw %}{{ $errors->has('email')? ' is-invalid':'' }}{% endraw %}"
        value="{% raw %}{{ old('email') }}{% endraw %}">

        @if ($errors->has('email'))
            <span class="invalid-feedback" role="alert">
                <strong>{% raw %}{{ $errors->first('email') }}{% endraw %}</strong>
            </span>
        @endif
    </div>
</div>

```

### Validation Boilerplate
```php

// Strings
'string' => 'required|string|max:256',
'boolean' => 'required|boolean',

// 10 Digit mobile number
'mobile' => 'required|digits:10|unique:users',

// Input should be Home or Office
'inThis' => ['required', Rule::in(['Home', 'Office'])],

// Should exists in categories table in id column
'parent' => 'integer|exists:categories,id',

// Should be an array, used with CSV input, check perpareForValidation for more info.
'value' => 'required|array',

// Multifile upload
'images.*' => 'required|image|mimes:jpeg|dimensions:ratio=1/1',

// Multifile upload limit
'images' => 'max:5',
```


### Error File Boilerplate
```html
@if ($flash = session('message'))
    <li class="list-group-item list-group-item-success" role="alert">{% raw %}{{ $flash }}{% endraw %}</li>
@endif

@if ($flash = session('error'))
    <li class="list-group-item list-group-item-danger" role="alert">{% raw %}{{ $flash }}{% endraw %}</li>
@endif

@if ($errors->any())
    <ul class="list-group">
        @foreach ($errors->all() as $err)
            <li class="list-group-item list-group-item-danger" role="alert">{% raw %}{{ $err}}{% endraw %}</li>
        @endforeach
    </ul>
@endif
```

### Bootstrap Boilerplate
```html
<!-- layouts.master -->
<!DOCTYPE html>
<html lang="en_US">
<head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">

    <meta name="csrf-token" content="@csrf">
    <title>@yield('title') - {% raw %}{{ config('app.name', 'Laravel') }}{% endraw %}</title>
    @include('layouts.stylesheets')
    @yield('style')
</head>
<body>
    @yield('content')
    @include('layouts.scripts')
    @yield('script')
</body>
</html>
```

```html
<!-- stylesheets.blade.php -->
<link rel="stylesheet" href="https://use.fontawesome.com/releases/v5.7.0/css/all.css">
<link href="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.2.1/css/bootstrap.min.css" rel="stylesheet">
<link href={% raw %}"{{ asset('css/app.css') }}"{% endraw %} rel="stylesheet">
```

```html
<!-- scripts.blade.php -->
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/jquery/3.3.1/jquery.min.js"></script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.4/umd/popper.min.js"></script>
<script type="text/javascript" src="https://cdnjs.cloudflare.com/ajax/libs/twitter-bootstrap/4.3.1/js/bootstrap.min.js"></script>
<script src={% raw %}"{{ asset('js/app.js') }}"{% endraw %}></script>
```

### Midlleware Boilerplate
```php
public function handle($request, Closure $next)
{
    if (!$request->user()->isAdmin()) {
        abort(403);
    }

    return $next($request);
}
```
### Return data with JSON header
```php
# Web.php
Route::get('/who', function() {
    $response = new stdClass();
    $response->status = "failed";
    $response->message = "Something went wrong";
    return response( json_encode($response), 200)
    ->header('Content-Type', 'application/json');
});
```

### Naming A Resource with a prepend in route
```php
resource('user', 'SchoolUserController', ['as' => 'school']);
/*
school.user.index
school.user.create
school.user.store
school.user.show
school.user.edit
school.user.update
school.user.delete
*/
```

### Open Graph Boilerplate
Working on it.

### Validation in API Controller with Custom Wrapper
```php

$validation = Validator::make($request->all(), [
    'mobile' => 'required|digits:10',
    'device_token' => 'required',
    'device_id' => 'required',
    'device_type' => 'required'
]);

if ($validation->fails()) {
    return [
        'status' => '422', // Validation error code (HTTP 422 = unprocessable entity)
        'results' => $validation->messages()
    ];
}
```