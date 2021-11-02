## Imagens Bitmap:
- Representam-se como matriz de pixéis;
- Não descrevem a imagem recorrendo a modelos matemáticos;
- As operações de edição normalmente pertimem criar e/ou modificar o aspeto dos pixéis que a constituem;<p>
![](https://wagnergaspar.com/wp-content/uploads/2021/05/3.png)
	
- O pixel é pois o elemento mais pequeno de resolução de uma imagem;
- O pixel aspect ratio é um valor numérico que representa a razão entre a largura do pixel e a sua altura;
- Os ___bitmaps___ igonaram a semântica (ou o significado) da informação que representa.

## Operações com imagens bitmap:
### Calculo do negativo da imagem:

O negativo de uma imagem é calculado subtraindo ao 255 o valor de vermelho ou verde ou azul.
O código abaixo se encontra escrito em _phyton_.
```python
from PIL import Image

image = Image.open("images/newYork.jpg")

#create a new image
negative_image = Image.new(image.mode, image.size, 'white')
negative_save.save("negative.jpg")

#negative algorithm
for i in range(0, image.size[0] - 1):
	for j in range(0, image.size[1]-1):

		# Get pixel value at (x,y) position of the image
		pixelColorVals = image.getpixel((i,j))

		# Invert color
		redPixel = 255 - pixelColorVals[0] # Negate red pixel
		greenPixel = 255 - pixelColorVals[1] # Negate green pixel
		bluePixel = 255 - pixelColorVals[1] # Negate blue pixel

		# Modify the image with inverted pixel values
		negative_image.putpixel((i,j),(redPixel, greenPixel, bluesPixel))

negative_image.save("negative.jpg")
```

### Calculo do Preto e Branco de uma imagem:

O codigo a baixo está escrito em _python_.
```python
from PIL import Image
from PIL import ImageEnhance

image = Image.open("images/newYork.jpg")
img_data = image.getdata()

lst = []
for i in img_data:
	lst.append(i[0]*0.2125 + i[1]*0.7174 + i[2]*0.0721)

new_img = Image.new("L", image.size)
new_img.putdata(lst)

new_img.save("black_white.jpg")
```

### Calculo da inversão da imagem:

O codigo a baixo esta escrito em _python_.
```python
# Load image
input_image = Image.open("images/newYork.jpg")
input_pixels = input_image.load()

# Create output image
output_image = Image.new("RGB", input_image.size)
draw = ImageDraw.Draw(output_image)

# Copy pixels
for x in range(output_image.width):
	for y in range(output_image.height):
		xp = input_image.width - x - 1
		draw.point((x, y), input_pixels[xp, y])

output_image.save("flip.jpg")
```

## Cor e codificação de cor:
### Conceitos Gerais:
- Luz: onde eletromagnética;
- Lus visível: entre os 400nm e os 700nm;
- Cor: comprimenton de onda da luz;
- Luz branca: todas as cores do arco iris;
- O olho humano sente o espectro de cores usando os cones e bastonentes.
### Modelo Aditivo e Subtractivo:
	Modelo aditivo:
	Descreve as cores emitidas ou projetadas, utilização em monitores.

![](https://i1.wp.com/www.hisour.com/wp-content/uploads/2018/03/RGB-color-model.jpg?w=720&ssl=1)

	Modelo Subtrativo:
	Descreve as cores impressas, utilização em impressoras.

![](https://i.loli.net/2019/07/05/5d1ec42acc42b55587.png)

### Modelo RGB:
- Três cores primárias: **vermelho**, **verde** e o **azul**;
- Ecrãs de vídeo (ex: computador, televisão) que restituem os tons pela adição das três cores primárias;
- Um tom é obtido através de uma combinação linear θ= ρ × R + γ × G + β × B, com (ρ, γ, β) ∈ [0, 1]^3;
- Considerando uma base de um byte para cada cor podemos modelar 2^8 x 2^8 x 2^8 = 2^24 = 1677716 cores;
- Uma imagem em modo 16 milhões de cores é conhecida por imagem em "true color".<p>

![](https://ramonpage.com/assets/images/posts/rgb-cube.png)

- **Origem**: ponto onde os três valores são iguas a 0 e que corresponde ao preto;
- **Vértice oposto**: ponto onde os valores das três coordenadas é máximo e por isso corresponde ao branco;
- **Vértice do cubo equistantes de duas cores primárias**: encontram-se as cores secundárias: amarelo, magenta e cião;
- Este modelo é **dependente dos periféricos** utilizados na aquisão e na representação.

![](http://4.bp.blogspot.com/-XSebXPhPo-Q/TV0BeHJUW7I/AAAAAAAAAAU/M5J9Sc7KH-0/s1600/sdabvksdlkf.jpg)

### Obter os canais de cor de uma imagem:
O código a baixo abaixo sepera os canais de cor de uma imagem. Esta escrito em _python_.
```python
from PIL import Image
import numpy as np

img = Image.open('image.png').convert('RGB')

def channel(img, n):
	""" n = 0: red, 1: green, 2: blue """
	a = np.array(img)
	a[:,:,(n != 0, n != 1, n != 2)] *= 0
	return Image.fromarray(a)

# RED IMAGE
red = channel(img, 0)
red.save("red.png")

# GREEN IMAGE
green = channel(img, 1)
green.save("green.png")

# BLUE IMAGE
blue = channel(img, 2)
blue.save("blue.png")
```

<p>O resultado final é o seguinte sem o preto e branco:

![](https://waltermattos.com/site/wp-content/uploads/2017/08/Poder_Curvas_Photoshop_Canais_RGB_Mistura.jpg)

### Modelo CMYK:
- Próprio para os **objetos que refletem luz**;
- Para obter as matrizes desejadas procede-se à **subtração das cores refeltida por uma superfício branca**;
- Seja uma fonte luminosa branca emitindo em direções de três filtros cião, magenta e amarelo:
	- **Ciano** (verde, azul): opôes-se à passagem do vermelho;
	- **Magenta**(vermelho, azul): opõe-se à passagem do verde;
	- **Amarelo**(verde, vermelho): opõe-se à passagem da cor azul.
	- 
### Formatos de ficheiros mais comuns:
	RGB:
	- jpg
	- png
	- gif
	- psd

<p>

	CMYK:
	- AI
	- PDF
	- EPS

### Modelo HSV:

- __H (Hue)__ -> Representa o tom.
- __S (Saturation)__ -> saturação da cor. Quanto mais baixo for a saturação, mais cizento é a cor. Quando a saturação é zero a cor é cizento.
- __V (Values)__ -> Representa a intensidade luminosidade. O brilho é determinado pelo grau de refletividade da superfície física que recebe a luz. Quanto maior for o brilho mais clara é a cor.

![](https://miro.medium.com/max/1400/0*YOMaPWRcXqAdKBbl.)

## Imagens Bitmap:
### Tamnho e Resolução:

	Profundidade -> número de bits para codificar um pixel.

<p>

	Podemos dividir as imagens bitmap em várias categorias:
	- imagens em dois níveis (preto e branco), com 1 bpp;
	- imagens em níveis de cizento, com 8 bpp;
	- imagens em cor indexada, com 8 bpp;
	- imagens "true color", com 24 bpp (+ componente alpha)

Sabendo a __largura__ e a __altura__, em pixéis, de uma imagem e a __profundidade__ de quantificação podemos calcular o __tamanho__ do ficheiro de uma imagem bitmap (não comprimido) com: <p>

![](https://latex.codecogs.com/gif.latex?%5Cdpi%7B300%7D%20%5Cbg_white%20%5Cfn_cm%20%5Chuge%20T%28KB%29%20%3D%5Cfrac%7Blargura%20%28pixel%29%20x%20altura%20%28pixel%29%20x%20porfundidade%20%28bits/pixel%29%7D%7B8%28bits/byte%29%20x%201024%28bytes/kB%29%7D)

__Resolução__ (ppp): número de pontos digitalizados, afixados ou imprimidos por uma unidade de largura.

### Imagens Bitmap - Vantagens:
- São capazes de produzir graduação de nuances e de cores muito finas;
- São constituídas por pixéis, o que __premite o tratamento ponto a ponto__ e são adaptadas a representação sobre ecrã ou impressão;
- São diretamente __guardadas na memória__, logo são __representadas muito rapidamente no ecrã__ (muito mais depressa do que as imagens vetoriais que, devem ser reconstituídas).

### Imagens Bitmap - Desvantagens:
- A __qualidade__ destas imagens está diretamente __dependente do material de aquiseção e de reprodução__ (por exemplo a resolução de ecrã, da impressora, do scanner);
- O facto de serem imagens de pontos __exige uma grande quantidade de espaço em memória__ (grande quantidade de pontos cujas características de cor são definidas individualmente).

### Imagens Bitmap - Entrelaçamento:
- As imagens bitmap podem permetir uma __visualização progressiva__ através da técnica de entrelaçamento. Mesmo com a redução de tamanho permitida pela indexação de cores uma imagem pode demorar um tempo considerável até poder ser visualizada.
- A técnica de entrelaçamento consiste em __reordenar as linhas das imagens, organizando-as em vários grupos__.
- A transmissão de imagens grupo a grupo permite que o utilizador comece a formar um ideia da imagem após apenas algumas linhas terem sido transmitidas.
- Esta característica pode ser observada durante o __carregamento de imagens transmitidas pela web__ quando o fluxo de dados é baixo.

![](https://i.stack.imgur.com/BtI3d.gif)

### Imagens Bitmap - Gif:
- Criada em 1980 pela Compuserve;
- Utilizada compressão sem perdas LZW;
- Profundidade de pixel não seperior a 8 bits;
- Otimizado para comrpessão de imagens contendo poucas cores diferentes e apresentando grandes quantidades de pixéis da mesma cor (logos, esquemas, diagramas a preto e branco, etx.);
- É adaptado a iamgens com forte constante e a texto mas não à fotografias realista;
- A variante GIF87a aceita entrelaçamento e a versão 89a jutna ainda a possibilidade de transparência e animação;
- Permite entrelaçamento;

### Imagens Bitmap - PNG:
- Formato mais recente que reúneas principais qualidades dos seus predecessores, eliminando a maiorria dos defeitos;
- Utiliza compressão sem perdas;
- Permite codificação até 48 bpp;
- Atinge níveis de comrpessão próximos des JPEG(mas sem perdas);
- Permite transparência por canal alpha;
- Este formato é livre (não utiliza qualquer algoritmo de domínio privado);

## Imagens Vetoriais:
	- A imagem vetorial é constituída por um conjunto de figuras elementares descrita por dados matemáticos.
	- Descrevem as diferentes figuras com objetos gráficos independentes uns ous outros.
	- Os objetos podem ser manipulados e transformados independentemente.

![](https://presentationteam.com/wp-content/themes/yootheme/cache/StickerYou_Blog_Vector-vs-Bitmap_600x400-3d19c944.webp)

### Imagens Vetoriais - Vantagens:
- As __informações__ são __descritas textualmente__ logo eficazmente comprimidas;
- O __tamanho da memória é independente do tamanho da imagem__;
- É possível __aplicar__ facilmente e __sem perda de precissão transformações geométricas__ (por exemplo: deslocamentos, translações, alteração de tamanho, rotações, etc...);
- Os diferentes __objetos__ podem ser __manipulados e transformados independentemente__ e com grande precisão;
- São __independentes dos periféricos e da resolução__, assim são automáticamente colocadas na escala para ser imprimida de forma precisa sobre o qualuqer periférico de saída.

### Imagens Vetoriais - Desvantagens:
- O tamanho do ficheiro varia em função da complexidade da imagem;
- Não podemos usar o formato vetorial para descerver uma imagem muito complexa, por exemplo fotografia;
- O __tempo de representação__ de uma imagem vetorial é __superior__ em relação a uma imagem bitmap (aumenta com a complexidade da imagem);
- Qualquer __perda ou corrupção__ no ficheiro leva à __perda de imagem na totalidade__;

### Imagens Vetoriais - Modelos Gráficos:
	Modelos geométricos: 📐

	Constituem o tipo de modelo gráfico mais comum e também o mais simples de desenvolver;
	São desenvolvidos à custa de formas geométricas 2D e 3D básicas que se designam por primitivas gráficas;
	As curvas e as superfícies curvas descrevem-se por intermédio de polinómios parametrizados.

<p>

	Modelos Sólido: 🧊
	
	Descrevem os objetos tridimensionais por meio de técnicas específicas:
	- CSG (Constructive Solid Geometry);
	- Superfícies de revolução;
	- Extrusão.

<p>

	Modelos Físico: 🌏
	
	Modelo com um grau muito elevado de precisão.
	Produzem imagens com muito realisto;
	Incluem descrição das forças, tensão e esforço aplicados aos objetos que constituem uma determinada cena.

<p>

	Modelos Empíricos: 🌤 🌊 🔥 🌳

	Descrevem os fenómenos naturais complexos:
	- Nuvens;
	- Ondas do mar;
	- Fogo;
	- Plantas
	Obtêm-se sobretudo por meio da observação da natureza.
	As técnicas utilizadas para a modelação empírica incluem as fractais e os sistemas de pratículas.
