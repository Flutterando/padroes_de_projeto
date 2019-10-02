# Identificadores / Nomenclatura

Identificadores são 3 basicamente em Dart.

```UpperCamelCase``` A primeira letra de cada nome é MAIUSCULOS incluindo a primeira.

```lowerCamelCase``` A primeira letra de cada nome é MAIUSCULOS menos a primeira.

```lowercase_with_underscores``` todas as letras são minusculo e as palavras são separadas por 1 undeline _ .

Quando usar UpperCamelCase?

Classes, enums, typedefs, and type parameters:

```dart
class SliderMenu { ... }

class HttpRequest { ... }

typedef Predicate<T> = bool Function(T value);
```

Isso inclui também classes destinadas a serem usadas nas anotações de metadados.

```dart
class Foo {
  const Foo([arg]);
}

@Foo(anArg)
class A { ... }

@Foo()
class B { ... }

```

Se o construtor da classe de anotação não usar parâmetros, convém criar uma constante lowerCamelCase separada para ela.

```dart
const foo = Foo();

@foo
class C { ... }
```

Para bibliotecas, pacotes, diretórios e arquivos usamos lowercase_with_underscores.


Alguns sistemas de arquivos não diferenciam maiúsculas de minúsculas; muitos projetos exigem que os nomes de arquivos sejam minúsculos. O uso de um caractere de separação permite que os nomes ainda sejam legíveis nesse formato. O uso de sublinhados como separador garante que o nome ainda seja um identificador Dart válido, o que pode ser útil se o idioma posteriormente suportar importações simbólicas.

Utilize assim:
```dart
library peg_parser.source_scanner;

import 'file_system.dart';
import 'slider_menu.dart';
```

Nunca assim:
```dart
library pegparser.SourceScanner;

import 'file-system.dart';
import 'SliderMenu.dart';
```

Nomeie os prefixos de importação usando lowercase_with_underscores.

```dart
import 'dart:math' as math;
import 'package:angular_components/angular_components'  as angular_components;
import 'package:js/js.dart' as js;
import 'dart:math' as Math;
import 'package:angular_components/angular_components' as angularComponents;
import 'package:js/js.dart' as JS;
```

Nomeie outros identificadores usando lowerCamelCase.


Os membros da classe, as definições de nível superior, as variáveis, os parâmetros e os parâmetros nomeados devem colocar em maiúscula a primeira letra de cada palavra, exceto a primeira, e não usar separadores.

```dart
var item;

HttpRequest httpRequest;

void align(bool clearItems) {
  // ...
}
```

Use lowerCamelCase para variáveis constantes, incluindo valores de enumeração.

Utilize assim:

```dart
const pi = 3.14;
const defaultTimeout = 1000;
final urlScheme = RegExp('^([a-z]+):');

class Dice {
  static final numberGenerator = Random();
}
```
Nunca assim:
```dart
const PI = 3.14;
const DefaultTimeout = 1000;
final URL_SCHEME = RegExp('^([a-z]+):');

class Dice {
  static final NUMBER_GENERATOR = Random();
}
```

Você pode usar SCREAMING_CAPS para obter consistência com o código existente, como nos seguintes casos:

- Quando adicionar código a um arquivo ou biblioteca que já usa SCREAMING_CAPS.

- Ao gerar código Dart paralelo ao código Java - por exemplo, em tipos enumerados gerados a partir de protobufs.

Porque não utilizar?

SCREAMING_CAPS parece ruim para muitos casos, particularmente valores de enumeração para coisas como cores CSS.

As constantes são frequentemente alteradas para variáveis ​​não-constantes finais, o que exigiria uma alteração de nome.

A propriedade de valores definida automaticamente em um tipo de enumeração é const e minúscula.
Coloque em maiúsculas acrônimos e abreviações com mais de duas letras, como palavras.

Acrônimos em maiúsculas podem ser difíceis de ler e vários acrônimos adjacentes podem levar a nomes ambíguos. Por exemplo, dado um nome que começa com HTTPSFTP, não há como saber se está se referindo ao HTTPS FTP ou HTTP SFTP.

Utilize assim:

```dart
HttpConnectionInfo
uiHandler
IOStream
HttpRequest
Id
DB
```

Nunca assim:
```dart
HTTPConnection
UiHandler
IoStream
HTTPRequest
ID
Db
```


- NÃO use um sublinhado principal para identificadores que não são particulares.
O Dart usa um sublinhado à esquerda em um identificador para marcar membros e declarações de nível superior como particulares. Isso treina os usuários a associar um sublinhado principal a um desses tipos de declaração. Eles vêem "_" e pensam "privado".

- Não há conceito de "privado" para variáveis locais (dentro de funçoes ou metodos), parâmetros ou prefixos de biblioteca. Quando um deles tem um nome que começa com um sublinhado, envia um sinal confuso ao leitor. Para evitar isso, não use sublinhados principais nesses nomes.


**Exceção:** um parâmetro não utilizado pode ser nomeado _, __, ___ etc. Isso acontece em retornos de chamada nos quais você recebe um valor, mas não precisa usá-lo. Dar a ele um nome que consiste apenas de sublinhados é a maneira idiomática de indicar que o valor não é usado.

- NÃO use letras de prefixo.
A notação húngara e outros esquemas surgiram na época do BCPL, quando o compilador não fez muito para ajudá-lo a entender seu código. Como o Dart pode informar o tipo, escopo, mutabilidade e outras propriedades de suas declarações, não há motivo para codificá-las nos nomes dos identificadores.

Utilize assim:
```dart
defaultTimeout
idade
```
Nunca assim:
```dart
kDefaultTimeout
intIdade
```

<!-- blank line -->
----
<!-- blank line -->

# Ordenação dos imports/exports

Para manter o preâmbulo do seu arquivo organizado, temos uma ordem prescrita na qual as diretivas devem aparecer. Cada "seção" deve ser separada por uma linha em branco.

Um atalho interessante no VSCode é ALT + SHIFT + O esse atalho organiza e remove os imports nao utilizados no documento.

FAÇA as importações "dart:" antes de outras importações.

```dart
import 'dart:async';
import 'dart:html';

import 'package:bar/bar.dart';
import 'package:foo/foo.dart';
```

FAÇA as importações de “pacote:” antes das importações relativas.


```dart
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'util.dart';
```
PREFERIR a importação externa de “pacote:” antes de outras importações.


Se você tiver várias importações de “pacotes:” para o seu próprio pacote, juntamente com outros pacotes externos, coloque o seu em uma seção separada após as externas.
```dart
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'package:my_package/util.dart';
```
Coloque os exports separados e depois de todos imports.

Utilize assim:
```dart
import 'src/error.dart';
import 'src/foo_bar.dart';

export 'src/error.dart';
```
Não assim:
```dart
import 'src/error.dart';
export 'src/error.dart';
import 'src/foo_bar.dart';
```
Ordene as sessões alfabeticamente.

Utilize assim:
<!-- background: #5A0000  -->
```dart
import 'package:bar/bar.dart';
import 'package:foo/foo.dart';

import 'foo.dart';
import 'foo/foo.dart';
```
Não assim:
```dart
import 'package:foo/foo.dart';
import 'package:bar/bar.dart';

import 'foo/foo.dart';
import 'foo.dart';
```


# Formatação

Como muitos idiomas, o Dart ignora os espaços em branco. No entanto, os humanos não. Ter um estilo de espaço em branco consistente ajuda a garantir que os leitores humanos vejam o código da mesma maneira que o compilador.

- Formate seu código usando o dartfmt.
A formatação é um trabalho tedioso e consome particularmente tempo durante a refatoração. Felizmente, você não precisa se preocupar com isso. Tanto o VSCode quando o Android Studio fornecem atalhos que formatam seu codigo no padrao dartfmt.

- Considere encurtar o nome de uma variável local ou elevar uma expressão para uma nova variável local. Em outras palavras, faça os mesmos tipos de modificação que você faria se estivesse formatando o código manualmente e tentando torná-lo mais legível.  

- EVITE linhas com mais de 80 caracteres.
Os estudos de legibilidade mostram que linhas longas de texto são mais difíceis de ler, porque seus olhos precisam viajar mais longe ao passar para o início da próxima linha. É por isso que jornais e revistas usam várias colunas de texto.


USE chaves entre todas as instruções de controle de fluxo.

Isso evita o problema dos outros pendentes.
```dart
if (isWeekDay) {
  print('Bike to work!');
} else {
  print('Go dancing or read a book!');
}
```
**Exceção:** Quando você tem uma instrução if sem cláusula else e a instrução if inteira se encaixa em uma linha, você pode omitir as chaves se preferir:
```dart
if (arg == null) return defaultValue;
```

Se o corpo passar para a próxima linha, use chaves (Isso ajuda e facilita os Merges do Git):

Utilize assim:

```dart
if (overflowChars != other.overflowChars) {
  return overflowChars < other.overflowChars;
}

```
Nunca assim:
```dart
if (overflowChars != other.overflowChars)
  return overflowChars < other.overflowChars;
```
