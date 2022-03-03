# Laravel translations Package
Sistema de traducciones para proyectos en Laravel con BackpackForLaravel.

## Requerimientos
Laravel-excel

```sh
composer require maatwebsite/excel
```

BackpackForLaravel
```sh
# require Backpack using Composer
composer require backpack/crud:"4.1.*"
composer require --dev backpack/generators

# run the installation command
php artisan backpack:install
```

## Configuración
Copiamos todos los archivos a nuestro proyecto actual y añadimos siguientes cambios a nuestro proyecto.

- app/Providers/AppServiceProvider.php
```sh
public function boot()
{
    LangFile::observe(LangFileObserver::class);
    LangSection::observe(LangSectionObserver::class);
    Language::observe(LanguageObserver::class);
}
```

- resources/views/vendor/base/inc/sidebar_content.blade.php
```sh
<li class="nav-item nav-dropdown">
    <a class="nav-link nav-dropdown-toggle" href="#"><i class="nav-icon la la-globe"></i>
        {{ trans('translationsystem.translations_nav') }}</a>
    <ul class="nav-dropdown-items">
        <li class='nav-item'><a class='nav-link' href='{{ backpack_url('language') }}'><i
                    class='nav-icon la la-flag-checkered'></i> {{ trans('translationsystem.languages_nav') }}</a></li>
        <li class='nav-item'><a class='nav-link' href='{{ backpack_url('lang-file') }}'><i
                    class="nav-icon lar la-file-alt"></i> {{ trans('translationsystem.lang_files_nav') }}</a></li>
        <li class='nav-item'><a class='nav-link' href='{{ backpack_url('lang-section') }}'><i
                    class="nav-icon las la-list"></i> {{ trans('translationsystem.lang_sections_nav') }}</a></li>
        <li class='nav-item'><a class='nav-link' href='{{ backpack_url('lang-translation') }}'><i
                    class="nav-icon las la-language"></i> {{ trans('translationsystem.lang_texts_nav') }}</a></li>
    </ul>
</li>
```

- routes/backpack/custom.php
```sh
Route::crud('lang-translation', 'LangTranslationCrudController');
Route::crud('lang-file', 'LangFileCrudController');
Route::crud('lang-section', 'LangSectionCrudController');
Route::crud('language', 'LanguageCrudController');

Route::get('lang-translation/texts/{lang?}/{file?}', 'LangTranslationCrudController@showTexts');
Route::post('lang-translation/update-texts', 'LangTranslationCrudController@updateTexts');
Route::get('lang-translation/make-translations-file', 'LangTranslationCrudController@makeTransletableFile');
```


Una vez copiados los archivos a otro proyecto ejecutamos el comando:
```sh
php artisan migrate
```
## License
© Copyright 20022-2099 Copyright.es - Todos los Derechos Reservados
