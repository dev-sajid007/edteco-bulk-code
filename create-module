Route::get('/get-object', function (Request $request) {

    $moduleList = $request->moduleList;
    $routeName = [];
    foreach ($moduleList as $module) {
        $url = $module['url'];
        $route = collect(Route::getRoutes())->first(function ($route) use ($url) {
            return $route->matches(request()->create($url));
        });
        $array = [
            'route' => $route->action['as']
        ];
        array_push($routeName, $array);
    }

    $mergedArray = array_map(function ($a, $b) {
        return array_merge($a, $b);
    }, $moduleList, $routeName);

    $arr = [];
    foreach ($mergedArray as $array) {
        $isReq = explode('/', $array['url']);
        Module::create([
            'name' => $array['name'],
            'url' => $array['url'],
            'route' => $array['route'],
            'is_request' => $isReq[0],
            'icon_class' => "mdi mdi-speedometer",
        ]);
    }
    dd("Done");
})->name('get-object');
