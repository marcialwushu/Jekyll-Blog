---
layout: post
title:  "Typed Properties Chegando no PHP 7.4"
date:   2018-11-12 02:20:31 -0200
categories: jekyll update
---




![](https://i0.wp.com/wp.laravel-news.com/wp-content/uploads/2017/07/php-leader.png?resize=2200%2C1125)


O  [Typed Properties 2.0 RFC](https://wiki.php.net/rfc/typed_properties_v2) foi aceito com 70 votos a favor e um voto contra. A maioria de 2/3 é necessária porque as Typed Properties são uma alteração da linguagem. A mudança de propriedade tipada é uma proposta do PHP 7.4.

>Com a introdução de tipos escalares e tipos de retorno, o PHP 7 aumentou muito o poder do sistema de tipagem do PHP. No entanto, atualmente não é possível declarar os tipagem de propriedades de classe, forçando os desenvolvedores a usar os métodos getter e setter para impor type contracts. Isso requer boilerplate code desnecessário, torna o uso menos ergonômico e prejudica o desempenho. Este RFC resolve esse problema introduzindo suporte para declarações de property type de primeira classe.

O RFC fornece um exemplo em que o objetivo é impor a segurança de tipos:

```php

class User {
    /** @var int $id */
    private $id;
    /** @var string $name */
    private $name;

    public function __construct(int $id, string $name) {
        $this->id = $id;
        $this->name = $name;
    }

    public function getId(): int {
        return $this->id;
    }
    public function setId(int $id): void {
        $this->id = $id;
    }

    public function getName(): string {
        return $this->name;
    }
    public function setName(string $name): void {
        $this->name = $name;
    }
}

```

Com o novo RFC aceito, esse código poderia ser funcionalmente equivalente da seguinte forma: "sem sacrificar a segurança da tipagem":

```php

class User {
    public int $id;
    public string $name;

    public function __construct(int $id, string $name) {
        $this->id = $id;
        $this->name = $name;
    }
}

```

Finalmente, aqui está um exemplo de todos os tipos válidos suportados em anotações executadas em tempo de execução para typed properties:

```php

class Example {
    // All types with the exception of "void" and "callable" are supported
    public int $scalarType;
    protected ClassName $classType;
    private ?ClassName $nullableClassType;

    // Types are also legal on static properties
    public static iterable $staticProp;

    // Types can also be used with the "var" notation
    var bool $flag;

    // Typed properties may have default values (more below)
    public string $str = "foo";
    public ?string $nullableStr = null;

    // The type applies to all properties in one declaration
    public float $x, $y;
    // equivalent to:
    public float $x;
    public float $y;
}

```

Está claro, dos enormes 70 votos a favor de 1 voto em oposição, que a equipe interna do PHP quer continuar introduzindo características de tipos, como segurança de tipos, na linguagem PHP.

No outro extremo do espectro, o PHP é utilizável em um paradigma completamente diferente de uma linguagem totalmente dinâmica abrangendo coerção de tipo. No entanto, com a continuação dos novos recursos de segurança de tipos introduzidos no PHP 7, não está claro como será prático usar uma abordagem totalmente dinâmica para escrever aplicativos PHP.

Por exemplo, se bibliotecas comuns como o Symfony e o framework PHPUnit implementarem este estilo de sintaxe, os consumidores que trabalham com essas bibliotecas devem seguir o exemplo e se adaptar ao novo mundo que é uma linguagem muito focada na tipagem. .

Alguns podem argumentar que forçar uma abordagem focada na tipagem é uma coisa boa e fará com que os programadores escrevam programas melhores com menos bugs. Junto com esse argumento, as ferramentas de análise estática podem muito bem ser capazes de detectar erros de tempo de execução antecipadamente.

Pelo menos para mim, esse tipo de discussão raramente tem estado em torno de evidências concretas de que a segurança de tipos aperfeiçoa o código, e mais em torno de cenários hipotéticos que dificultam discernir se a segurança de tipos torna o código “melhor”.

Não sei se a divisão de estilos de programação se ampliará entre programadores dinâmicos e fortemente tipados. Para mim, parece inevitável que os recursos de linguagem evitem estilos de programação dinâmicos devido à crescente preferência de desenvolvedores que desejam uma linguagem fortemente tipada.

O que isso significa para aqueles que querem programar sem tipos? Só o tempo dirá, mas eu prevejo que pelo menos uma pequena maioria de programadores que deseje que a linguagem permaneça com suas raízes dinâmicas irá procurar outras linguagens.

## Saber mais

Para saber mais, a proposta [rfc: typed_properties_v2](https://wiki.php.net/rfc/typed_properties_v2) é a melhor fonte de informações precisas neste momento. Uma [implementação](https://github.com/php/php-src/pull/3313) já está em andamento para typed properties.

[ARTIGO ORIGINAL](https://laravel-news.com/php7-typed-properties)

