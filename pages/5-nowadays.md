---
layout: center
align: center
transition: fade
--- 

# Tá, mas e a parte tećnica?

Ferramentas? Conceitos? Como que procede com isso?

> Muita variavel pra pouca constante - Reis, Daniel


---
transition: fade-out
layout: whoami
image: https://pbs.twimg.com/profile_banners/1514035325089333254/1676263789/1500x500
handle: "Não existe motivo pra manter a codebase suja em 2025"
full_name: "Desenvolvimento Inteligente"
---


# Desenvolvimento Inteligente


Sua primeira missão vai ser sempre ter um ambiente organizado.

<v-clicks>

Com **"ambiente"**, eu me refiro a ferramental do tipo:

- Ferramentas de Linting, Type Checking e "Typo Checking"
- Ferramentas de Testes Unitários/Aceitação/E2E/Arch
- Priorizar seguranca com pacotes atualizados (Composer/NPM)

</v-clicks>


<v-click>

Então no geral, podemos entender que:

</v-click>

<div class="mt-5" v-click>

> Padronizar o projeto de todo mundo vai fazer a bagunça ser menor!

</div>



---
layout: whoami
image: https://i.imgur.com/KEibtMj.png
handle: "Code Styling"
full_name: "1. Laravel Pint"
---


# Laravel Pint

Reorganize a codebase de um jeito inteligente e minimalista.


> $ composer require laravel/pint --dev

```json
{
    "preset": "laravel",
    "rules": {
        "simplified_null_return": true,
        "array_indentation": false,
        "new_with_parentheses": {
            "anonymous_class": true,
            "named_class": true
        }
    }
}
```

Execute com: 

> $ vendor/bin/pint



---
handle: "Code Refactor"
full_name: "2. RectorPHP"
layout: whoami
image: https://i.imgur.com/n1hDw2i.png
---

# RectorPHP

Refatore seu código instantâneamente adicionando tipágens óbvias.


> $ composer require rector/rector --dev

```php {*}{maxHeight:'250px'}
return RectorConfig::configure()
    ->withPaths([
        __DIR__.'/app',
    ])
    ->withImportNames(
      importShortClasses: false, 
      removeUnusedImports: true
    )
    ->withPreparedSets(
        deadCode: true,
        codeQuality: true,
        codingStyle: true,
        typeDeclarations: true,
        privatization: true,
        instanceOf: true,
        earlyReturn: true,
        strictBooleans: true,
        carbon: true,
        rectorPreset: true
    )
    ->withSkip([
        DeclareStrictTypesRector::class,
        ChangeOrIfContinueToMultiContinueRector::class,
    ])
    ->withSets([
        LaravelSetList::LARAVEL_ARRAYACCESS_TO_METHOD_CALL,
        LaravelSetList::LARAVEL_ARRAY_STR_FUNCTION_TO_STATIC_CALL,
        LaravelSetList::LARAVEL_CODE_QUALITY,
        LaravelSetList::LARAVEL_COLLECTION,
        LaravelSetList::LARAVEL_CONTAINER_STRING_TO_FULLY_QUALIFIED_NAME,
        LaravelSetList::LARAVEL_ELOQUENT_MAGIC_METHOD_TO_QUERY_BUILDER,
        LaravelSetList::LARAVEL_FACADE_ALIASES_TO_FULL_NAMES,
        LaravelSetList::LARAVEL_IF_HELPERS,
        LaravelSetList::LARAVEL_LEGACY_FACTORIES_TO_CLASSES,
    ]);
```

Execute com: 

> $ vendor/bin/rector src --dry-run

---
handle: "Test Runner"
full_name: "3. PestPHP"
layout: whoami
image: https://i.imgur.com/d2MELaX.png
---

# PestPHP

Escreva testes simples e elegantes pra sua codebase.

> $ composer require pestphp/pest --dev --with-all-dependencies

```php {*}{maxHeight:'250px'}
arch()->preset()->php();
arch()->preset()->security()->ignoring('md5');

arch()
    ->expect('App')
    ->toUseStrictTypes()
    ->not->toUse(['die', 'dd', 'dump']);
 
arch()
    ->expect('App\Models')
    ->toBeClasses()
    ->toExtend('Illuminate\Database\Eloquent\Model')
    ->toOnlyBeUsedIn('App\Repositories')
    ->ignoring('App\Models\User');
 
arch()
    ->expect('App\Http')
    ->toOnlyBeUsedIn('App\Http');
 
arch()
    ->expect('App\*\Traits')
    ->toBeTraits();
```

Execute com: 

> $ vendor/bin/pest
---
handle: "Garantindo a porra toda"
full_name: "4. CI/CD"
layout: whoami
image: https://i.imgur.com/d2MELaX.png
---

# Continuous Integration

Garanta a confiabilidade das mudanças na sua pipeline.

> Num tem comando pra isso, mas o ChatGPT te ajuda nessa 

```yaml {*}{maxHeight:'250px'}
name: Continuous Integration

on:
  push:
    branches:
      - main
      - develop
  pull_request:
    branches:
      - main
      - develop

concurrency:
  group: ${{ github.workflow }}-${{ github.event.pull_request.number || github.ref }}
  cancel-in-progress: true

env:
  PHP_VERSION: 8.3
  PHP_EXTENSIONS: mbstring,pdo,xml,ctype,fileinfo,json,curl,openssl,dom,zip
  PHP_INI_PROPERTIES: post_max_size=256M,upload_max_filesize=256M

jobs:
  setup:
    name: Setup PHP
    runs-on: ubuntu-latest
    outputs:
      combined-key: ${{ steps.prepare-env.outputs.combined-key }}
    steps:
      - name: Checkout code
        uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2

      - name: Prepare environment and composer data
        id: prepare-env
        run: |
          composer_hash=${{ hashFiles('**/composer.lock') }}
          os_lower=$(echo ${{ runner.os }} | tr '[:upper:]' '[:lower:]')
          arch_lower=$(echo ${{ runner.arch }} | tr '[:upper:]' '[:lower:]')
          combined_key="${os_lower}-${arch_lower}-composer-${composer_hash}"
          echo "combined-key=${combined_key}" >> "$GITHUB_OUTPUT"

      - name: Setup PHP
        uses: shivammathur/setup-php@9e72090525849c5e82e596468b86eb55e9cc5401 # v2.32.0
        with:
          php-version: ${{ env.PHP_VERSION }}
          extensions: ${{ env.PHP_EXTENSIONS }}
          ini-values: ${{ env.PHP_INI_PROPERTIES }}
          coverage: xdebug
          tools: composer:v2

      - name: Install composer dependencies
        uses: ramsey/composer-install@57532f8be5bda426838819c5ee9afb8af389d51a # v3.0.0
        with:
          composer-options: "--prefer-dist"
          custom-cache-key: ${{ steps.prepare-env.outputs.combined-key }}
  pint:
    name: Perform Pint format
    runs-on: ubuntu-latest
    needs:
      - setup
    steps:
      - name: Checkout code
        uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2

      - name: Setup PHP
        uses: shivammathur/setup-php@9e72090525849c5e82e596468b86eb55e9cc5401 # v2.32.0
        with:
          php-version: ${{ env.PHP_VERSION }}
          extensions: ${{ env.PHP_EXTENSIONS }}
          ini-values: ${{ env.PHP_INI_PROPERTIES }}
          coverage: xdebug
          tools: composer:v2

      - name: Install composer dependencies
        uses: ramsey/composer-install@57532f8be5bda426838819c5ee9afb8af389d51a # v3.0.0
        with:
          composer-options: "--prefer-dist"
          custom-cache-key: ${{ needs.setup.outputs.combined-key }}

      - name: Run Pint
        env:
          XDEBUG_MODE: off
        run: |
          composer run-script test:pint

  rector:
    name: Perform Rector Check
    runs-on: ubuntu-latest
    needs:
      - setup
    steps:
      - name: Checkout code
        uses: actions/checkout@11bd71901bbe5b1630ceea73d27597364c9af683 # v4.2.2

      - name: Setup PHP
        uses: shivammathur/setup-php@9e72090525849c5e82e596468b86eb55e9cc5401 # v2.32.0
        with:
          php-version: ${{ env.PHP_VERSION }}
          extensions: ${{ env.PHP_EXTENSIONS }}
          ini-values: ${{ env.PHP_INI_PROPERTIES }}
          coverage: xdebug
          tools: composer:v2

      - name: Install composer dependencies
        uses: ramsey/composer-install@57532f8be5bda426838819c5ee9afb8af389d51a # v3.0.0
        with:
          composer-options: "--prefer-dist"
          custom-cache-key: ${{ needs.setup.outputs.combined-key }}

      - name: Run Rector
        run: |
          composer run-script test:rector





  pest:
    name: Run Pest Tests
    runs-on: ubuntu-latest
    needs:
      - setup
    steps:
      - name: Checkout
        uses: actions/checkout@v4

      - name: Setup PHP
        uses: shivammathur/setup-php@v2
        with:
          php-version: ${{ env.PHP_VERSION }}
          extensions: ${{ env.PHP_EXTENSIONS }}
          ini-values: ${{ env.PHP_INI_PROPERTIES }}
          coverage: xdebug
          tools: composer:v2

      - name: Setup Node
        uses: actions/setup-node@v4
        with:
          node-version: '22'
          cache: 'npm'

      - name: Install Node Dependencies
        run: npm i

      - name: Add Flux Credentials Loaded From ENV
        run: composer config http-basic.composer.fluxui.dev "${{ secrets.FLUX_USERNAME }}" "${{ secrets.FLUX_LICENSE_KEY }}"

      - name: Install Dependencies
        run: composer install --no-interaction --prefer-dist --optimize-autoloader

      - name: Copy Environment File
        run: cp .env.example .env

      - name: Generate Application Key
        run: php artisan key:generate

      - name: Build Assets
        run: npm run build

      - name: Run Tests
        run: composer run-script test

```

Execute com: 

> Greetz: @usb777 - Gabriel Vieira (gh: @gvieira18)

---
layout: center
align: center
transition: fade
---

# Beleza, e o que mais eu posso fazer de imediato?

Com a codebase levemente organizada, a gente melhora os contextos!

> Toda vez que alguém usa um número mágico numa codebase, o Marcel sente uma tristeza momentanea :/

---
handle: "POR FAVOR NINGUÉM SABE O QUE É STATUS = 2"
full_name: "Enumerators"
layout: whoami
image: https://i.imgur.com/BC5zdhQ.png
---

# Crie Enums!

Isso literalmente explica regras de negócios situacionais :')


```php {*}{maxHeight:'250px'}
// Validação manual dos números mágicos
if (!in_array($newStatus, [0, 1, 2, 3, 4])) {
    return response()->json([
      'error' => 'Status inválido'
    ], 400);
}

// vs

enum OrderStatus: int
{
    case Pending = 0;
    case Approved = 1;
    case Shipped = 2;
    case Delivered = 3;
    case Canceled = 4;
}

// Usando tryFrom para tentar converter o inteiro em Enum
$statusEnum = OrderStatus::tryFrom($newStatus);
if (!$statusEnum) {
    return response()->json([
      'error' => 'Status inválido'
    ], Response::HTTP_BAD_REQUEST);
}

```

---
handle: "Não custa 5 minutos do seu dia."
full_name: "Composer Update"
layout: whoami
image: https://i.imgur.com/BC5zdhQ.png
---

# Atualize seus pacotes

A não ser que tu queira ser "ownado" do jeito mais bobo possível.

> $ composer outdated

```bash {*}{maxHeight:'250px'}
Color legend:
- patch or minor release available - update recommended
- major release available - update possible

Direct dependencies required in composer.json:
driftingly/rector-laravel                   2.0.4   2.0.5    Rector upgrades rules for Laravel Framework
filament/filament                           3.3.14  3.3.17   A collection of full-stack components for accelerated Laravel app development.
filament/notifications                      3.3.14  3.3.17   Easily add beautiful notifications to any Livewire app.
filament/spatie-laravel-tags-plugin         3.3.14  3.3.17   Filament support for `spatie/laravel-tags`.
laravel/framework                           12.14.0 12.16.0  The Laravel Framework.
laravel/pulse                               1.4.1   1.4.2    Laravel Pulse is a real-time application performance monitoring tool and dashboa...
laravel/sail                                1.43.0  1.43.1   Docker files for running a basic Laravel application.
laravel/telescope                           5.7.0   5.8.0    An elegant debug assistant for the Laravel framework.
openai-php/client                           0.10.3  0.13.0   OpenAI PHP is a supercharged PHP API client that allows you to interact with the...
phpunit/phpunit                             11.5.20 12.1.6   The PHP Unit Testing framework.
rector/rector                               2.0.16  2.0.17   Instant Upgrade and Automated Refactoring of any PHP code
spatie/laravel-medialibrary                 11.12.9 11.13.0  Associate files with Eloquent models

Transitive dependencies not required in composer.json:
anourvalar/eloquent-serialize               1.3.1   1.3.3    Laravel Query Builder (Eloquent) serialization
aws/aws-sdk-php                             3.343.9 3.343.22 AWS SDK for PHP - Use Amazon Web Services in your PHP project
brick/math                                  0.12.3  0.13.1   Arbitrary-precision arithmetic library
filament/actions                            3.3.14  3.3.17   Easily add beautiful action modals to any Livewire component.
filament/forms                              3.3.14  3.3.17   Easily add beautiful forms to any Livewire component.
filament/infolists                          3.3.14  3.3.17   Easily add beautiful read-only infolists to any Livewire component.
filament/support                            3.3.14  3.3.17   Core helper methods and foundation code for all Filament packages.
filament/tables                             3.3.14  3.3.17   Easily add beautiful tables to any Livewire component.
filament/widgets                            3.3.14  3.3.17   Easily add beautiful dashboard widgets to any Livewire component.
google/apiclient-services                   0.396.0 0.397.0  Client library for Google APIs
kirschbaum-development/eloquent-power-joins 4.2.3   4.2.4    The Laravel magic applied to joins.
laravel/socialite                           5.20.0  5.21.0   Laravel wrapper around OAuth 1 & OAuth 2 libraries.
nikic/php-parser

```

> Por uma "bobeira" dessa de versão de algo, o 4chan foi de arrasta 🎉

---
layout: center
align: center
transition: fade
---

# Uma breve história

De uma certa consultoria polêmica na qual eu to autorizado a falar.

> Até pq se tem tweet, tem historia kkkkkkkkkkkkkkkk 
