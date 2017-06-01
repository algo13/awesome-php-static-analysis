# Awesome static analysis for PHP

A curated list of static analysis tools for PHP.

*   [Awesome PHP](https://github.com/ziadoz/awesome-php) - #Code Analysis
*   [Awesome static analysis](https://github.com/mre/awesome-static-analysis) - #PHP
*   [Static analysis tools for PHP](https://github.com/exakat/php-static-analysis-tools)

## Table of Contents

*   Standalone
    *   [Bugs finders](#bugs-finders)
        *   [Bugs finders(Specialized)](#bugs-findersspecialized)
        *   [Bugs finders(Security)](#bugs-finderssecurity)
    *   [Coding standards](#coding-standards)
    *   [Compatibility](#compatibility)
        *   [Compatibility Fixers](#compatibility-fixers)
    *   [Fixers](#fixers)
    *   [Metrics](#metrics)
        *   [API documentation generator](#api-documentation-generator)
        *   [Benchmark](#benchmark)
*   [Tools package](#tools-package)
*   [DIY(Libraries)](#diylibraries)
*   [Online](#online)
*   [SaaS](#saas)
*   [Misc](#misc)

## Standalone

### Bugs finders

*   [php -l](http://php.net/manual/en/features.commandline.options.php) - Syntax check only (lint)

    Windows:
    ```bat
    for /r . %%f in (*.php,*.inc,*.html) do php -l "%%f"
    ```

    Linux:
    ```sh
    $ find ./ -name "*.php" | xargs -n1 php -l
    ```

    *   [PHP Parallel Lint](https://github.com/JakubOnderka/PHP-Parallel-Lint) - This tool check syntax of PHP files faster than serial check with fancier output.
    *   [PHPLint](https://github.com/overtrue/phplint) - A tool that can speed up linting of php files by running several lint processes at once.


| Name                                                  | Run                                                  | Target  | phar | Depend                | Notes                                                           |
|-------------------------------------------------------|------------------------------------------------------|---------|------|-----------------------|-----------------------------------------------------------------|
| [Phan](https://github.com/etsy/phan)                  | PHP7+<br>[php-ast](https://github.com/nikic/php-ast) |         | YES  | `nikic/php-ast`       |                                                                 |
| [PHPStan](https://github.com/phpstan/phpstan)         | PHP7+                                                | PHP5.6+ | NO   | `nikic/php-parser`    |                                                                 |
| [PHPMD](https://github.com/phpmd/phpmd)               | PHP5.3+                                              |         | YES  | `pdepend/pdepend`     | cleancode,codesize<br>controversial,design<br>naming,unusedcode |
| [PHPSA](https://github.com/ovr/phpsa)                 | PHP5.5+                                              | PHP5.2+ | YES  | `nikic/php-parser`    |                                                                 |
| [php-nag](https://github.com/algo13/php-nag)          | PHP5.4+                                              | PHP5.2+ | YES  | `nikic/php-parser`    | Deprecated functions,<br>Fall through, etc ...                  |
| [Tuli](https://github.com/ircmaxell/Tuli)             | PHP5.5+                                              |         | NO   | `ircmaxell/php-types` | Latest commit on 24 Oct 2015                                    |
| [magniffer](https://github.com/magento-ecg/magniffer) |                                                      |         | NO   | `nikic/php-parser`    | Latest commit on 16 Dec 2015                                    |
| [PHPLinter](https://github.com/robotis/PHPLinter)     |                                                      |         | NO   |                       | Latest commit on 16 Aug 2012                                    |

*   [17eyes](https://github.com/17eyes/17eyes) - Written in Haskell.
*   [Yasca](http://yasca.org) - Including [PHPLint](http://www.icosaedro.it/phplint/).
*   [SonarSource](https://www.sonarsource.com/)
    *   [SonarQube](http://www.sonarqube.org) - Open platform to manage code quality.
    *   [SonarLint](http://www.sonarlint.org) - An extension to your favorite IDE.
    *   [SonarLint for Command Line](http://www.sonarlint.org/commandline/) - CLI tool.
*   [Php Inspections (EA Extended)](https://github.com/kalessil/phpinspectionsea) - [PhpStorm](https://www.jetbrains.com/phpstorm/) plugin.

#### Bugs finders(Specialized)

| Name                                                                          | phar | Depend                 | Notes                                                                                |
|-------------------------------------------------------------------------------|------|------------------------|--------------------------------------------------------------------------------------|
| [PHPCPD](https://github.com/sebastianbergmann/phpcpd)                         | YES  |                        | Copy/Pasted Detector(CPD).                                                           |
| [PHPDCD](https://github.com/sebastianbergmann/phpdcd)                         | YES  |                        | Dead Code Detector(DCD).                                                             |
| [Pattern Detector](https://github.com/Halleck45/DesignPatternDetector)        | NO   | `halleck45/phpmetrics` | Design Pattern Detector.                                                             |
| [PhpCodeAnalyzer](https://github.com/wapmorgan/PhpCodeAnalyzer)               | NO   |                        | Finds usage of non-built-in extensions.                                              |
| [PHP Assumption](https://github.com/rskuipers/php-assumptions)                | NO   | `nikic/php-parser`     | Finds [weak assumptions](http://rskuipers.com/entry/from-assumptions-to-assertions). |
| [PHP Unlocker](http://emanuilslavov.com/php-unlocker/)                        | NO   | `nikic/php-parser`     | Scan [ADOdb](http://adodb.org/dokuwiki/doku.php) code for unintended table locks.    |
| [twig-lint](https://github.com/asm89/twig-lint)                               | YES  |                        | Standalone [Twig](http://twig.sensiolabs.org/) linter.                               |


#### Bugs finders(Security)

| Name                                                                    | UI      | Depend              | Notes                                                                               |
|-------------------------------------------------------------------------|---------|---------------------|-------------------------------------------------------------------------------------|
| [phpvulhunter](https://github.com/OneSourceCat/phpvulhunter)            | Browser | `nikic/php-parser`  | Vulnerabilities                                                                     |
| [RIPS](https://github.com/ripsscanner/rips)                             | Browser |                     | Vulnerabilities<br>(OOP not supported)                                              |
| [psecio/parse](https://github.com/psecio/parse)                         | CLI     | `nikic/php-parser`  | A PHP Security Scanner.                                                             |
| [VisualCodeGrepper](https://github.com/nccgroup/VCG)                    | GUI     |                     | Written in VisualBasic.                                                             |
| [Eir](https://github.com/Lixody/Eir)                                    | CLI     | `nikic/php-parser`  | Written in C#.                                                                      |
| [PHP Reaper](https://github.com/emanuil/php-reaper)                     | CLI     | `nikic/php-parser`  | Scan ADOdb code for SQL Injections.                                                 |
| [TaintPHP](https://github.com/olivo/TaintPHP)                           | CLI     | `nikic/php-parser`  | Static Taint Analysis.                                                              |
| [Side Channel Analyzer](https://github.com/olivo/side-channel-analyzer) | CLI     | `olivo/TaintPHP`    | Search for [Side-channel attack](https://en.wikipedia.org/wiki/Side-channel_attack) |
| [phantm](https://github.com/colder/phantm)                              | CLI     |                     | Latest commit on 8 Oct 2012                                                         |
| [Pixy](https://github.com/oliverklee/pixy)                              | CLI     |                     | Latest commit on 20 Dec 2014                                                        |

*   [XSS code sniffer](http://pecl.php.net/package/taint) - Taint extension.
*   [versionscan](https://github.com/psecio/versionscan) - Security check for `PHP Version`.
*   [Scanner for PHP.ini](https://github.com/psecio/iniscan) - Security check for `php.ini`.
*   [Security Advisories Checker](https://security.sensiolabs.org/) ([Web Service / API](https://security.sensiolabs.org/api), [Online Checker](https://security.sensiolabs.org/check)) - Security check for `composer.lock`.
    *   [PHP Security Advisories Database](https://github.com/FriendsOfPHP/security-advisories)
        *   [SensioLabs Security Checker](https://github.com/sensiolabs/security-checker) - CLI tool.
        *   [Roave Security Advisories](https://github.com/Roave/SecurityAdvisories) - The checks are executed when running `composer` command.
*   [WPScan](https://wpscan.org/) - [WordPress](https://wordpress.com/) vulnerability scanner.

### Coding standards

*   [EasyCodingStandard](https://github.com/Symplify/EasyCodingStandard) - Best intro tool for Coding Standards. Combine PHP_CodeSniffe and PHP-CS-Fixer.
*   [PHP CS Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer) - The PSR-1 and PSR-2 Coding Standards **fixer**.
*   [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) - `phpcs`(Checker), `phpcbf`(Fixer).
*   [PHPCheckstyle](https://github.com/PHPCheckstyle/phpcheckstyle)

### Compatibility

| Name                                                                    | phar | Depend                      | Notes                                               |
|-------------------------------------------------------------------------|------|-----------------------------|-----------------------------------------------------|
| [PHPCompatibility](https://github.com/wimg/PHPCompatibility)            |      | `squizlabs/PHP_CodeSniffer` | Required `PHP_CodeSniffer`.                         |
| [PHPCodeFixer](https://github.com/wapmorgan/PhpCodeFixer)               | NO   |                             | Deprecated functions, variables and ini directives. |
| [PHP Migration](https://github.com/monque/PHP-Migration)                | YES  | `nikic/php-parser`          | PHP version migration and compatibility checking.   |
| [php7cc](https://github.com/sstalle/php7cc)                             | YES  | `nikic/php-parser`          | PHP7 Compatibility Checker.                         |
| [php7mar](https://github.com/Alexia/php7mar)                            | NO   |                             | PHP7 Migration Assistant Report.                    |

#### Compatibility Fixers

*   [Transphpile: A PHP 7 to PHP 5.6 transpiler](https://github.com/jaytaph/Transphpile)
*   [PHP 5.4 Short Array Syntax Converter](https://github.com/thomasbachem/php-short-array-syntax-converter) - array() to [].
*   [Namespacer](https://github.com/zendframework/Namespacer) - PHP Class converter to namepaces.([Namespacing Old Classes](https://framework.zend.com/manual/2.4/en/migration/namespacing-old-classes.html))

### Fixers

*   [PHP Refactoring Browser](https://github.com/QafooLabs/php-refactoring-browser)
*   [PHPDoc to Type Hint](https://github.com/dunglas/phpdoc-to-typehint)
*   [PHP Transpiler](https://github.com/original-brownbear/php-transpiler) - PHP minifier.

### Metrics

*   [PHPLOC](https://github.com/sebastianbergmann/phploc) - line of codes.
*   [PHP Metrics](https://github.com/Halleck45/PhpMetrics)


*   [Mondrian](https://github.com/Trismegiste/Mondrian)
*   [PhpDependencyAnalysis](https://github.com/mamuz/PhpDependencyAnalysis)
*   [PHP Depend](https://github.com/pdepend/pdepend)
*   [Dissect](https://github.com/jakubledl/dissect)
*   [dePHPend](https://github.com/mihaeu/dephpend)
*   [phpCallGraph](http://phpcallgraph.sourceforge.net/)

#### API documentation generator

*   [phpDocumentor](https://www.phpdoc.org/)
*   [ApiGen](https://github.com/apigen/apigen)
*   [Sami](https://github.com/FriendsOfPHP/Sami)
*   [phpDox](https://github.com/theseer/phpdox)
*   [Doxygen](http://www.stack.nl/~dimitri/doxygen/)
    *   [doxygen-php-filters](https://github.com/AbcAeffchen/doxygen-php-filters)

#### UML

*   [phUML](https://github.com/jakobwesthoff/phuml) - Require [Graphviz](http://www.graphviz.org/)
*   [php-plantumlwriter](https://github.com/davidfuhr/php-plantumlwriter) - Require [PlantUML](http://plantuml.com/)
*   [PHP_UML](http://pear.php.net/package/PHP_UML/)

#### Benchmark

*   [PhpBench](https://github.com/phpbench/phpbench)
*   [Ubench](https://github.com/devster/ubench)
*   [~~Athletic~~](https://github.com/polyfractal/athletic)

## Tools package

*   [GrumPHP](https://github.com/phpro/grumphp) - Checks code on every commit.
*   [Qafoo Quality Analyzer](https://github.com/Qafoo/QualityAnalyzer) - Quality Analyzer is a tool to visualize metrics and source code.
*   [PHPQA CLI](https://github.com/EdgedesignCZ/phpqa) - A tool for running QA tools(`phploc`, `phpcpd`, `phpcs`, `pdepend`, `phpmd`, `phpmetrics`).

## DIY(Libraries)

*   [php-ast](https://github.com/nikic/php-ast) - Extension exposing PHP7 AST(abstract syntax tree).
*   [PHP Parser](https://github.com/nikic/PHP-Parser) - A PHP parser written in PHP.
    *   [Deptrac](https://github.com/sensiolabs-de/deptrac)
    *   [Better Reflection](https://github.com/Roave/BetterReflection)
    *   [PHP Manipulator](https://github.com/schmittjoh/php-manipulator)
    *   [PHPSandbox](https://github.com/Corveda/PHPSandbox)
    *   [PHP-CFG](https://github.com/ircmaxell/php-cfg)
        *   [PHP-Types](https://github.com/ircmaxell/php-types)
    *   [phpDocumentor/Reflection](https://github.com/phpDocumentor/Reflection)
*   [PHP Token Reflection](https://github.com/Andrewsville/PHP-Token-Reflection)
*   [PHP Coupling Detector](https://github.com/akeneo/php-coupling-detector)
*   [php-parser](https://github.com/glayzzle/php-parser) - A NodeJS library.

## Online

*   [devbug](http://www.devbug.co.uk/) - PHP Static Code Analysis.
*   [3v4l.org](https://3v4l.org/) - run code in 150+ php & hhvm versions

## SaaS

*   [PHPCI](https://www.phptesting.org/)
*   [Scrutinizer](https://scrutinizer-ci.com/)
*   [SensioLabsInsight](https://insight.sensiolabs.com/)
*   [Code Climate](https://codeclimate.com) - `PHP Code Sniffer`, `PHP Mess Detector`, `Phan`.
*   [Codacy](https://www.codacy.com/)
*   [Checkmarx](http://lp.checkmarx.com/php-code-analysis/) - PHP Code Security Analysis.
*   [RIPS](https://www.ripstech.com/) - Automated Security Analysis for PHP Code.
*   [Bliss](https://blissai.com)

## Misc

*   [Box](https://github.com/box-project/box2) - An application for building and managing Phars.
*   [PHP Semantic Versioning Checker](https://github.com/tomzx/php-semver-checker)
*   [PHP_CodeCoverage](https://github.com/sebastianbergmann/php-code-coverage)
*   [PHP_CodeBrowser](https://github.com/mayflower/PHP_CodeBrowser) - Generates a browsable representation of PHP code where sections with violations found by quality assurance tools such as `PHP_CodeSniffer` or `PHPMD` are highlighted.
*   [HHVM](http://hhvm.com/) ([Tools](https://docs.hhvm.com/hack/tools/))
*   [hussar](https://github.com/wayfair/hussar) - PHP static analysis with HHVM.
*   [PHP Analysis](https://github.com/cwi-swat/php-analysis) - PHP Analysis in Rascal (PHP AiR).
*   [PHPPHP](https://github.com/ircmaxell/PHPPHP) - A PHP VM implementation in PHP.
*   [php.js](https://github.com/niklasvh/php.js) - PHP VM in JavaScript.

