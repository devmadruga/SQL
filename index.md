# Banco de Dados de um e-commerce

* ### Objetivo:

Criar perguntas (e READS que gerem as respostas) importantes com base no BD fornecido (este é um BD exemplo).

* ### Download e/ou visualização dos dados:

**SE VOCÊ DESEJA FAZER O DOWNLOAD DOS ARQUIVOS DE DADOS, ACESSE [AQUI](https://github.com/devmadruga/SQL/tree/main/e-commerce).**

**Se quiser acesso rápido aos dados do BD, veja: [customer.csv](https://github.com/devmadruga/SQL/blob/main/e-commerce/customer.csv), [product.csv](https://github.com/devmadruga/SQL/blob/main/e-commerce/product.csv) e [sales.csv](https://github.com/devmadruga/SQL/blob/main/e-commerce/sales.csv)**

* ### Um print das tabelas contidas neste BD:

![Image](https://github.com/devmadruga/SQL/blob/gh-pages/bd-ecommerce-esquema-tabelas.jpg)

* ### PERGUNTAS CRIADAS:
OBSERVAÇÃO: Respostas obtidas para PostgreSQL.

> "GERENTE DE MARKETING:"
Qual o número de clientes abaixo de 36 anos? Qual o número de clientes entre 36 e 54 anos? Qual o número de clientes acima de 54 anos?

`SELECT region, CASE WHEN age > 54 THEN 'Cat 3'`

`WHEN age < 36 then 'Cat 1'`

`ELSE 'Cat 2' END AS age_group, COUNT(*)`

`FROM customer GROUP BY region, age_group`

`ORDER BY region, COUNT DESC;`


> GERENTE DE CADEIA DE SUPRIMENTOS:
Uma lista com os 5 produtos mais vendidos na East region.

`SELECT c.product_id, d.product_name, c.total_q_sold`

`FROM (SELECT e.product_id, SUM(e.quantity) AS total_q_sold`

`FROM (SELECT a.*, b.region`

`FROM sales AS a`

`LEFT JOIN customer AS b`

`ON a.customer_id=b.customer_id) AS e WHERE e.region = 'East' GROUP BY e.product_id) AS c`

`LEFT JOIN product AS d`

`ON c.product_id = d.product_id`

`ORDER BY total_q_sold DESC`

`LIMIT 5;`


> GERENTE DE CADEIA DE SUPRIMENTOS:
Uma lista com os 5 produtos menos vendidos na South region.

`SELECT c.product_id, d.product_name, c.total_q_sold`

`FROM (SELECT s.product_id, SUM(s.quantity) AS total_q_sold`

`FROM (SELECT a.*, b.region`

`FROM sales AS a`

`LEFT JOIN customer AS b`

`ON a.customer_id=b.customer_id) AS s WHERE s.region = 'South' GROUP BY s.product_id) AS c`

`LEFT JOIN product AS d`

`ON c.product_id = d.product_id`

`ORDER BY total_q_sold ASC`

`LIMIT 5;`

> GERENTE FINANCEIRO:
Perda de receita total em função dos discontos.

`SELECT SUM(discount*sales) AS total_discount FROM sales;`

> GERENTE FINANCEIRO:
Receita total e desconto para cada produto.

`SELECT product_id, SUM(discount*sales) AS discount, (SUM(sales) - SUM(discount*sales)) AS revenue, SUM(discount*sales)/(SUM(sales) - SUM(discount*sales)) AS ratio FROM sales`

`GROUP BY product_id`

`ORDER BY ratio DESC;`







## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/devmadruga/SQL/edit/gh-pages/index.md) to maintain and preview the content for your website in Markdown files.

Whenever you commit to this repository, GitHub Pages will run [Jekyll](https://jekyllrb.com/) to rebuild the pages in your site, from the content in your Markdown files.

### Markdown

Markdown is a lightweight and easy-to-use syntax for styling your writing. It includes conventions for

```markdown
Syntax highlighted code block

# Header 1
## Header 2
### Header 3

- Bulleted
- List

1. Numbered
2. List

**Bold** and _Italic_ and `Code` text

[Link](url) and ![Image](src)
```

For more details see [GitHub Flavored Markdown](https://guides.github.com/features/mastering-markdown/).

### Jekyll Themes

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/devmadruga/SQL/settings/pages). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://docs.github.com/categories/github-pages-basics/) or [contact support](https://support.github.com/contact) and we’ll help you sort it out.
