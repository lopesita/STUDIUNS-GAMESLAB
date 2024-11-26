# TENDÊNCIAS E IMPACTOS DE MERCADO NA TRAJETÓRIA DE LANÇAMENTOS DE JOGOS DA STEAM - Projeto Aplicado I

Seja bem-vindo ao **Projeto Aplicado I** da **Universidade Presbiteriana Mackenzie**!

Este projeto foi desenvolvido por **Italo Aparecido Lopes** e **Rafael Augusto Alba**. Ele tem como foco a análise de tendências de mercado relacionadas a lançamentos de jogos na plataforma Steam.

## Objetivo do Projeto

Este trabalho tem como objetivo analisar a evolução dos gêneros de jogos publicados na plataforma Steam, identificando tendências de crescimento e declínio entre 1997 e 2024.

## Descrição do Dataset

O dataset contém as seguintes informações principais sobre os jogos:

- **Título do Jogo** (*title*)
- **Gênero** (*genres*)
- **Desenvolvedor** (*developer*)
- **Publisher** (*publisher*)
- **Avaliação Geral** (*overall_review*)
- **Preço com Desconto** (*discounted_price*)

## Funcionalidades

Este projeto oferece as seguintes funcionalidades:

- Análise dos principais gêneros de jogos lançados ao longo dos anos.
- Estudo das avaliações dos usuários e como elas impactam as tendências de jogos.
- Exame dos preços e sua relação com a aceitação do público.

## Como Usar

1. Clone este repositório:

    ```bash
    git clone https://github.com/seu-usuario/seu-repositorio.git
    ```

2. Instale as dependências necessárias (Python/R):

    ```bash
    pip install -r requirements.txt
    ```

3. Explore os notebooks disponíveis para visualizar as análises e gráficos:

    - **PA1.ipynb**: Contém as principais análises realizadas sobre o dataset da Steam, com gráficos e insights sobre gêneros de jogos, preços e avaliações.

## Conclusões

A pesquisa mostrou que gêneros como **Ação** e **Aventura** continuam a dominar o mercado, enquanto gêneros emergentes, como **Indie**, ganham força, impulsionados pela acessibilidade de ferramentas e plataformas. No entanto, ainda há questões não totalmente exploradas, como a influência dos preços elevados em certos gêneros. 

A relação entre a aceitação do público e o preço de determinados jogos merece uma análise mais profunda, já que o custo pode ser um fator decisivo nas avaliações negativas. Jogos de alto custo que prometem experiências premium, mas não atendem às expectativas, podem sofrer avaliações negativas mais acentuadas.

A análise dos dados permitiu identificar tendências de crescimento em gêneros como **Casual** e **Indie**, que atraem novos jogadores e mantêm uma base sólida devido aos preços mais acessíveis. Contudo, o custo elevado de jogos mais complexos pode explicar parte das críticas negativas, sugerindo a necessidade de balanceamento entre preço e qualidade percebida.

### Considerações Finais

Com essas considerações, a pesquisa caminha para uma análise mais completa sobre o mercado de jogos, investigando como fatores econômicos, como o preço, impactam a recepção de títulos específicos e gêneros. O tema central de como as tendências de lançamento e popularidade dos jogos evoluem será enriquecido ao integrar essas variáveis, proporcionando um entendimento mais robusto do mercado de jogos digitais.

## Código

```python

# Limpar e converter a coluna 'discounted_price' para numérico
steam_data['discounted_price'] = pd.to_numeric(
    steam_data['discounted_price'].replace({'Free': 0, '₹': '', 'NaN': None}, regex=True),
    errors='coerce'
)

# Extrair o gênero antes da primeira vírgula
steam_data['primary_genre'] = steam_data['genres'].apply(lambda x: x.split(',')[0] if pd.notnull(x) else None)

# Agrupar por gênero e calcular o preço médio para os 10 gêneros mais caros
top_10_genres = steam_data.groupby('primary_genre')['discounted_price'].mean().sort_values(ascending=False).head(10)

# Plotar os 10 principais gêneros por preço médio
import matplotlib.pyplot as plt

plt.figure(figsize=(10, 6))
top_10_genres.plot(kind='bar', color='skyblue')
plt.title('Top 10 Gêneros por Preço Médio com Desconto')
plt.ylabel('Preço Médio')
plt.xlabel('Gêneros')
plt.xticks(rotation=45, ha='right')
plt.tight_layout()
plt.show()

Link para apresentação dos resultados: https://discord.com/channels/1282459294436163594/1282459294436163598/1310780191626498129
