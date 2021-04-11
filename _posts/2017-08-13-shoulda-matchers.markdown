---
layout: default
title: Simplifique seus testes com Shoulda Matchers
permalink: testing-shoulda-matchers
---

# Simplificando seus testes com os Shoulda Matchers

*Criado por Ana Schwendler, [@anaschwendler](https://twitter.com/anaschwendler)*.
*Traduzido por Frankyston Lins, [@frankyston](https://twitter.com/frankyston)*.

**Este guia pressupõe que você já tenha criado um aplicativo Rails Girls** [**seguindo o guia de desenvolvimento**](/app).
**O tutorial RSpec por** [**este guia**](/testing-rspec)
**e o tutorial de comentários** [**este guia**](/commenting)

[Shoulda Matchers](https://github.com/thoughtbot/shoulda-matchers) é uma gem de teste Ruby, que fornece linhas de comandos compatíveis com RSpec e Minitest que testam a funcionalidade comum do Rails. Esses testes seriam, de outro modo, muito mais longos, mais complexos e propensos a erros.

**Instrutor(a):** Fale sobre testes e Desenvolvimento Orientado a Comportamento.

## *1.* Adicione a gem Shoulda Matchers

Abra seu `Gemfile` e adicione esta linha ao grupo `:test` acima da tag end:

{% highlight ruby %}
group :test do
  ...
  gem 'shoulda-matchers'
end
{% endhighlight %}

e execute
{% highlight sh %}
bundle install
{% endhighlight %}
para instalar a gem.

**Instrutor(a):** Fale sobre 'googlear' a saída do terminal.

## *2.* Ajuste seu `rails_helper.rb`

No nosso caso, estaremos usando o RSpec para testar nosso projeto, então precisamos dizer ao nosso `rails_helper.rb` que estamos usando o Shoulda Matchers:

Coloque acima da tag end (verifique o recuo):

{% highlight ruby %}
Shoulda::Matchers.configure do |config|
  config.integrate do |with|
    # Escolha um framework de teste:
    with.test_framework :rspec
    with.library :rails
  end
end
{% endhighlight %}

**Instrutor(a):** Fale sobre porque estamos ajustando a gem dentro de `rails_helper.rb`.

No seu terminal execute
{% highlight sh %}
rspec spec/models/idea_spec.rb
{% endhighlight %}

Deve mostrar que o nosso teste está funcionando.

## *3.* Testando!

É bem simples testar usando o Shoulda Matchers.
Para o nosso primeiro teste já afirmamos que uma ideia tem muitos comentários, no [**Comentários para o tutorial Rails Girls App**](/commenting)

Para testar se isso está funcionando corretamente, podemos adicionar as linhas abaixo ao nosso `spec/lib/idea_spec.rb`, acima do primeiro teste que criamos:

{% highlight ruby %}
describe "associations" do
  it{ is_expected.to have_many(:comments) }
end
{% endhighlight %}

Este é um teste de associação.

**Instrutor(a):** Fale sobre testes de associação.

## *4.* Desenvolvimento Orientado a Testes

**Instrutor(a):** Fale sobre o TDD e como começamos a adicionar recursos ao nosso aplicativo testando-o primeiro.

Outro recurso que podemos adicionar ao nosso aplicativo é criar ideias sempre nomeadas. Como poderíamos fazer isso? Vamos começar dizendo que as idéias sempre devem ter um nome.

Vamos começar criando um teste para isso. Podemos fazer isso adicionando as seguintes linhas ao nosso `spec/lib/idea_spec.rb`:

{% highlight ruby %}
describe "validations" do
  it{ is_expected.to validate_presence_of :name }
end
{% endhighlight %}

adicione-o abaixo do nosso teste de associação.

Depois disso, execute no seu terminal
{% highlight sh %}
rspec spec/models/idea_spec.rb
{% endhighlight %}

Deve nos dar que não estamos validando adequadamente (e realmente não estamos). Então, para validar isso, precisamos adicionar as seguintes linhas ao nosso modelo, para que possamos validar a presença do nome em nossa Idéia.

{% highlight ruby %}
validates :name, presence: true
{% endhighlight %}
adicione-o abaixo da nossa declaração has_many.

agora volte ao seu terminal e execute
{% highlight sh %}
rspec spec/models/idea_spec.rb
{% endhighlight %}

Deve dar o resultado positivo.

## *5.* Faça isso você mesmo!

Você pode continuar este tutorial fazendo um teste para validar a presença de uma descrição?

Você consegue imaginar outros testes para fazer?

Feliz testes!

{% include other-guides.md page="testing-shoulda-matchers" %}
