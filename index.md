## EMR en el DCA

1. Descargar _dataset_ del repositorio y comprimirlo
```
git clone https://github.com/st0263eafit/bigdata.git 
cd bigdata/datasets && zip –r dataset * 
```
2. Copiar el _dataset_ al **DCA** y descomprimirlo en una carpeta
```
scp dataset.zip marami26@192.168.10.116:/home/marami26/dataset.zip 
ssh marami26@192.168.10.116 
mkdir datasets && unzip dataset.zip -d datasets 
```
3. Crear carpeta para almacenar los datasets en mi directorio de **HDFS**
```
hdfs dfs -mkdir /user/marami26/datasets 
```
4. Copiar el _dataset_ del **DCA** al directorio de **HDFS**
```
hdfs dfs –copyFromLocal datasets/* /user/marami26/datasets/ 
```

**Resultados**
* Terminal
![terminal](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/dca/terminal.png)

* Ambari
![ambari](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/blob/master/imagenes/dca/ambari.png)

## Welcome to GitHub Pages

You can use the [editor on GitHub](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/edit/master/index.md) to maintain and preview the content for your website in Markdown files.

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

Your Pages site will use the layout and styles from the Jekyll theme you have selected in your [repository settings](https://github.com/Mateo-RH/TopicosTelematica-BigDataLab/settings). The name of this theme is saved in the Jekyll `_config.yml` configuration file.

### Support or Contact

Having trouble with Pages? Check out our [documentation](https://help.github.com/categories/github-pages-basics/) or [contact support](https://github.com/contact) and we’ll help you sort it out.
