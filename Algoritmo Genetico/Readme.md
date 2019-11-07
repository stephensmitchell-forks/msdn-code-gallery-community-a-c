# Algoritmo Genetico
## Requires
- Visual Studio 2017
## License
- MIT
## Technologies
- C#
- Windows Forms
## Topics
- Artificial Intelligence
## Updated
- 03/10/2017
## Description

<p><span style="font-size:x-small">Los algoritmos gen&eacute;ticos forman parte de la inteligencia artificial y est&aacute;n inspirados en la forma de trabajar de la evoluci&oacute;n y la gen&eacute;tica. Creamos un cromosoma digital, en el cual cada gen es
 una caracter&iacute;stica que necesitamos para la soluci&oacute;n del problema. Las posibles soluciones evolucionan y se seleccionan de forma similar a la selecci&oacute;n natural. Existen diversas formas de llevar a cabo la selecci&oacute;n. A veces, tambi&eacute;n
 suceden mutaciones que pueden ser beneficiosas o perjudiciales. El cruce entre los organismos se usa para crear la generaci&oacute;n siguiente.</span></p>
<p>Partimos de una poblaci&oacute;n de flores en las que el usuario puede seleccionar algunas caracter&iacute;sticas, color, tama&ntilde;o y altura del tallo. Al inicio las flores crecer&aacute;n al azar. Estas se reproducir&aacute;n entre s&iacute;, e incluso
 habr&aacute; mutaciones. Poco a poco, conforme avancen las generaciones y si todo sale bien, tendremos una poblaci&oacute;n de flores similares a las que solicit&oacute; el usuario.<br>
<br>
&nbsp; &nbsp; &nbsp;Tenemos tres Group Boxes y dentro de cada unos de ellos tres Radio Buttons y debajo un Label.<br>
&nbsp; &nbsp; &nbsp;El grupo de Altura tendr&aacute; los Radio Buttons Alto,Medio y Bajo con los names: rbAlto, rbMedio y rbBajo.<br>
&nbsp; &nbsp; &nbsp;El grupo Color de la flor tendr&aacute; los Radio Buttons Rojo, Azul y Amarillo con los names: rbRojo, rbAzul y rbAmarillo.<br>
&nbsp; &nbsp; &nbsp;El grupo Tama&ntilde;o de la flor tendra los Radio Buttons Peque&ntilde;o, Normal y Grande con los names: rbPequeno, rbNormal y rbGrande, a la etiqueta la llamaremos lblGeneracion.<br>
<br>
&nbsp; &nbsp; &nbsp;Crearemos la clase Flores y en ella colocaremos la informaci&oacute;n del cromosoma, el valor de adaptaci&oacute;n y la posici&oacute;n de la flor.<br>
<br>
&nbsp; &nbsp; &nbsp;La variable X guarda la posici&oacute;n de la flor, en la variable adaptaci&oacute;n se guarda el nivel de adaptaci&oacute;n de la flor. El cromosoma va a tener 6 genes: altura, color, color del tallo, ancho del tallo, tama&ntilde;o de la
 flor, tama&ntilde;o del centro de la flor.</p>
<p><span><span>Contamos con un arreglo al que llamamos cromosoma. El cromosoma va a tener seis genes. Cada posici&oacute;n en el arreglo equivale a un cromosoma. El primer gen se encarga de la altura de la flor, y su rango es de 10 a 300. En el segundo codificamos
 el color de la flor. El valor de 0 indicar&aacute; rojo, el valor de 1 es azul, y el valor de 2, amarillo. El color del tallo se asigna en el tercer gen y tiene tres posibles tonos de verde. El ancho del tallo es otra caracter&iacute;stica que podemos colocar;
 para este caso el rango de valores ser&aacute; de 5 a 15. El quinto gen es el tama&ntilde;o de la flor, va desde 20 hasta 80. El ultimo gen es el centro de la flor y el rango es de 5 a 15.<br>
Una vez definidos los datos creamos dos propiedades CoorX para el dato X y Adaptaci&oacute;n para nuestra variable adaptaci&oacute;n.<br>
<br>
&nbsp; &nbsp; &nbsp;El primer dato del arreglo flores, lo llamamos poblaci&oacute;n. En este arreglo colocaremos los objetos que representan a la flores.<br>
&nbsp; &nbsp; &nbsp;Nuestra poblaci&oacute;n de flores es de 10. La variable generaci&oacute;n lleva la cuenta del n&uacute;mero de generaciones transcurridas de la aplicaci&oacute;n. Ademas, hay dos enteros, los cuales ser&aacute;n usados para guardar los
 &iacute;ndices del arreglo donde se encuentran las flores que se han seleccionado como padres para la siguiente<strong> generaci&oacute;n.</strong><br>
</span></span></p>
<h1><em style="font-size:10px"><img id="170870" src="170870-captura.jpg" alt="" width="811" height="630">&nbsp;</em></h1>
<p><img id="170871" src="170871-captura1.jpg" alt="" width="816" height="627"></p>
<div class="scriptcode">
<div class="pluginEditHolder" pluginCommand="mceScriptCode">
<div class="title"><span>C#</span></div>
<div class="pluginLinkHolder"><span class="pluginEditHolderLink">Editar script</span>|<span class="pluginRemoveHolderLink">Remove</span></div>
<span class="hidden">csharp</span>
<pre class="hidden">using System;

namespace AlgoritmosGeneticos
{
 /// &lt;summary&gt;
 /// Descripci&oacute;n breve de Flores.
 /// &lt;/summary&gt;
 public class Flores
 {
  // Variables necesarias para la clase
  private int x; // Posici'on en la ventana
  private double adaptacion; // Nivel de adaptacion del organismo
  

  // Creamos el cromosoma de la flor
  // 0-Altura
  // 1-Color de la flor
  // 2-Color del tallo
  // 3-Ancho del tallo
  // 4-Tama&ntilde;o de la flor
  // 5-Tama&ntilde;o del centro de la flor

  public int[] cromosoma=new int[6];

  // Creamos las propiedades
  public int CoordX
  {
   set {x=value;}
   get {return x;}
  }

  public double Adaptacion
  {
   set {adaptacion=value;}
   get {return adaptacion;}
  }


  public Flores()
  {
   //
   // TODO: agregar aqu&iacute; la l&oacute;gica del constructor
   //
  
  }

 }
}


     Creamos un objeto de tipo Random, Luego tenemos un ciclo, donde recorreremos todas las flores de nuestra poblaci&oacute;n. Creamos el objeto flor y asignamos la posici&oacute;n donde le corresponde. Procedemos a rellenar el cromosoma. A cada gen del cromosoma, le colocamos un valor aleatorio de acuerdo con el rango que puede tener. As&iacute; iniciamos una poblaci&oacute;n creada al azar, que deber&aacute; evolucionar hacia el tipo de caracter&iacute;sticas seleccionadas por el usuario. Cuando se ejecute la aplicaci&oacute;n, aparecer&aacute;n diez flores diferentes en la ventana.



// Inicializamos los valores de los cromosomas.



// Arreglo de flores
  public Flores[] poblacion=new Flores[10];
  private System.Windows.Forms.Label lblGeneracion;
  private int generacion=0;
  private int iPadreA,iPadreB;


public Form1()
  {
   //
   // Necesario para admitir el Dise&ntilde;ador de Windows Forms
   //
   InitializeComponent();

   //
   // TODO: agregar c&oacute;digo de constructor despu&eacute;s de llamar a InitializeComponent
   //

   Random random=new Random(unchecked((int)DateTime.Now.Ticks));
   for(int n=0;n&lt;10;n&#43;&#43;)
   {
    Flores temp=new Flores();
    poblacion[n]=temp;
    poblacion[n].CoordX=n*80&#43;40;
    
    // Inicializamos el cromosoma con valores al azar
    
    // La altura va de 10 a 300
    poblacion[n].cromosoma[0]=random.Next(10,300);

    // El color de la flor. 0-rojo, 1-azul, 2-amarillo
    poblacion[n].cromosoma[1]=random.Next(0,3);

    // El color del tallo. Diferentes tonos de verde
    poblacion[n].cromosoma[2]=random.Next(0,3);

    // El ancho del tallo. De 5 a 15
    poblacion[n].cromosoma[3]=random.Next(5,15);

    // El tamano de la flor. De 20 a 80
    poblacion[n].cromosoma[4]=random.Next(20,80);

    // El tamano del centro de la flor. De 5 a 15
    poblacion[n].cromosoma[5]=random.Next(5,15);
   }

  }


Primero pintamos el suelo. Luego con un ciclo recorremos todas la flores, pintando una por una seg&uacute;n sus caracter&iacute;sticas. Se `pinta el tallo, dependiendo de su color. El color se guarda en el tercer gen, es decir el que se encuentra en el &iacute;ndice 2. Al usar el gen en el &iacute;ndice 0, vemos su altura, y el valor del gen con &iacute;ndice 3 nos sirve para colocar el ancho del tallo.

Para pintar la flor, utilizamos el circulo. Llevamos a cabo la selecci&oacute;n del color usando el el valor contenido en el gen 1. Con el valor del gen con &iacute;ndice 4, colocamos el tama&ntilde;o., Todos los centros de las flores se pintan del mismo color, en esta caso, un tono naranja oscuro. El tama&ntilde;o del centro lo obtenemos en el gen con &iacute;ndice 5. Despu&eacute;s de pintar todas las flores, actualizamos la etiqueta colocando el valor actual de la generaci&oacute;n.


private void Form1_Paint(object sender, System.Windows.Forms.PaintEventArgs e)
  {
   // Pintamos un suelo
   e.Graphics.FillRectangle(Brushes.DarkGreen,0,550,800,50);

   // Pintamos las flores
   for(int n=0;n&lt;10;n&#43;&#43;)
   {
    // 0-Altura
    // 1-Color de la flor
    // 2-Color del tallo
    // 3-Ancho del tallo
    // 4-Tama&ntilde;o de la flor
    // 5-Tama&ntilde;o del centro de la flor

    // pintamos el tallo
      
    // vemos el color del tallo
    if(poblacion[n].cromosoma[2]==0)
     e.Graphics.FillRectangle(Brushes.DarkGreen,
      poblacion[n].CoordX,550-poblacion[n].cromosoma[0],
      poblacion[n].cromosoma[3],poblacion[n].cromosoma[0]);
    else if(poblacion[n].cromosoma[2]==1)
     e.Graphics.FillRectangle(Brushes.Green,
      poblacion[n].CoordX,550-poblacion[n].cromosoma[0],
      poblacion[n].cromosoma[3],poblacion[n].cromosoma[0]);
    else if(poblacion[n].cromosoma[2]==2)
     e.Graphics.FillRectangle(Brushes.LightGreen,
      poblacion[n].CoordX,550-poblacion[n].cromosoma[0],
      poblacion[n].cromosoma[3],poblacion[n].cromosoma[0]);

    // Pintamos la flor
    //Color cflor=new Color();
    Color cflor=new Color(); 
    
    if(poblacion[n].cromosoma[1]==0)
     cflor=Color.Red;
    else if(poblacion[n].cromosoma[1]==1)
     cflor=Color.Blue;
    else if(poblacion[n].cromosoma[1]==2)
     cflor=Color.Yellow;

    e.Graphics.FillEllipse(new SolidBrush(cflor),
     poblacion[n].CoordX&#43;poblacion[n].cromosoma[3]/2-poblacion[n].cromosoma[4]/2,
     550-poblacion[n].cromosoma[0]-poblacion[n].cromosoma[4]/2,
     poblacion[n].cromosoma[4],poblacion[n].cromosoma[4]);

    //Pintamos el centro de la flor
    e.Graphics.FillEllipse(Brushes.DarkOrange,
     poblacion[n].CoordX&#43;poblacion[n].cromosoma[3]/2-poblacion[n].cromosoma[5]/2,
     550-poblacion[n].cromosoma[0]-poblacion[n].cromosoma[5]/2,
     poblacion[n].cromosoma[5],poblacion[n].cromosoma[5]);
   }

   lblGeneracion.Text=&quot;Generacion: &quot;&#43;generacion.ToString();
  }


El ciclo en donde se lleva a cabo el proceso de la evoluci&oacute;n se incorpora por medio del Timer. Cada vez que el Timer genere el evento, se realizar&aacute; todo el proceso necesario para crear una nueva generaci&oacute;n. El evento del Timer se llama Tick, y, en su handler, colocamos el siguiente c&oacute;digo:

private void timer1_Tick(object sender, System.EventArgs e)
  {
   // Calculamos la adaptacion
   CalculaAdaptacion();

   // Seleccionamos a los padres
   SeleccionaPadres();

   // Hacemos el crossover y la mutacion
   Crossover();

   // Acutalizamos la generacion
   generacion&#43;&#43;;

   // Redibujamos la ventana
   this.Invalidate();
  }

En esa funci&oacute;n se invocar&aacute;n a varias funciones especializadas que nos ayudan con el proceso. La primera funci&oacute;n CalculaAdaptacion() sirve para que se calcule el nivel de adaptaci&oacute;n de cada flor. Luego SeleccionaPadres() obtiene los dos padres que se utilizar&aacute;n para crear la siguiente generaci&oacute;n. La funci&oacute;n de CrossOver() hace el intercambio gen&eacute;tico y se encarga de la mutaci&oacute;n. Despu&eacute;s, se incrementa la variable de generaci&oacute;n y se manda a redibujar la ventana.


No existe una f&oacute;rmula para el c&aacute;lculo de la adaptaci&oacute;n,; cada aplicaci&oacute;n tendr&aacute; su propia forma de llevar a cabo ese c&aacute;lculo. A veces, puede ser tan sencillo como una resta; otras, se necesitar&aacute;n mecanismos m&aacute;s complicados. Nuestra funci&oacute;n CalculaAdaptacion() queda de la siguiente manera:

private void CalculaAdaptacion()
  {
   // Variables para las opciones del usuario
   int altura,color,tamano;
   altura=color=tamano=0;

   // Variables necesarias para el calculo
   double Aaltura,Acolor,Atamano;
   Aaltura=Acolor=Atamano=0.0;

   // Obtnemos la altura deseada por el usuario
   if(rbBajo.Checked==true)
    altura=0;
   else if(rbMedio.Checked==true)
    altura=1;
   else if(rbAlto.Checked==true)
    altura=2;

   // Obtenemos el color deseado por el usuario
   if(rbRojo.Checked==true)
    color=0;
   else if(rbAzul.Checked==true)
    color=1;
   else if(rbAmarillo.Checked==true)
    color=2;

   // Obtenemos el tama&ntilde;o de la flor deseado por el usuario
   if(rbPequeno.Checked==true)
    tamano=0;
   else if(rbNormal.Checked==true)
    tamano=1;
   else if(rbGrande.Checked==true)
    tamano=2;


   // Recorremos toda la poblaci&oacute;n para encontrar su adaptaci&oacute;n
   for(int n=0;n&lt;10;n&#43;&#43;)
   {
    // Checamos el nivel de adaptaci&oacute;n para la altura
    if(altura==0) // rango 10 a 100
     Aaltura=poblacion[n].cromosoma[0]/100;
    else if(altura==1) // rango 100 a 200
     Aaltura=poblacion[n].cromosoma[0]/200;
    else if(altura==2) // rango 200 a 300
     Aaltura=poblacion[n].cromosoma[0]/300;

    if(Aaltura&gt;1.0)
     Aaltura=1/Aaltura;

    // Checamos el nivel de adaptaci&oacute;n del color
    if(color==poblacion[n].cromosoma[1])
     Acolor=1.0;
    else
     Acolor=0.0;

    // Checamos el nivel de adaptaci&oacute;n del tama&ntilde;o de la flor
    if(tamano==0) // rango 20 a 40
     Atamano=poblacion[n].cromosoma[4]/40;
    else if(tamano==1) // rango 40 a 60
     Atamano=poblacion[n].cromosoma[4]/60;
    else if(tamano==2) // rango 60 a 80
     Atamano=poblacion[n].cromosoma[4]/80;

    if(Atamano&gt;1.0)
     Atamano=1/Atamano;

    // Calculamos el valor final de adaptaci&oacute;n
    poblacion[n].Adaptacion=(Aaltura&#43;Acolor&#43;Atamano)/3.0;

   }

  }


Para calcular la adaptaci&oacute;n,se calculan tres valores, uno para cada caracter&iacute;stica que queremos comparar y, luego, se saca el promedio entre ellos, Dentro de la funci&oacute;n, en primer lugar, reconocemos cu&aacute;les son las caracter&iacute;sticas que ha solicitado el usuario, mediante la lectura de los Radio Buttons. Luego recorreremos toda la poblaci&oacute;n y calculamos el valor de adaptaci&oacute;n para cada flor. Como podemos ver, cada caracter&iacute;stica tiene su propia forma de calcular su nivel de adaptaci&oacute;n; luego, sacamos el promedio entre ellos

La funci&oacute;n para la selecci&oacute;n de los padres es SeleccionaPadres(). Esta funci&oacute;n resulta muy sencilla, simplemente, selecciona las dos flores con valor valor de adaptaci&oacute;n. Los &iacute;ndices donse se encuentran son guardados en las variables iPadreA e iPadreB.

private void SeleccionaPadres()
  {
   // Seleccionamos los dos mejores
   // Modelo elitista
   
   iPadreA=iPadreB=0;

   // Encontramos el padre A
   for(int n=0;n&lt;10;n&#43;&#43;)
   {
    if(poblacion[n].Adaptacion&gt;poblacion[iPadreA].Adaptacion)
     iPadreA=n;
   }

   // Encontramos el padre B
   for(int n=0;n&lt;10;n&#43;&#43;)
   {
    if(poblacion[n].Adaptacion&gt;poblacion[iPadreB].Adaptacion &amp;&amp; iPadreA!=n)
     iPadreB=n;
   }

  }

La funci&oacute;n para el cruce de los cromosomas. En la funci&oacute;n CrossOver(), tomamos los padres seleccionados y creamos una nueva generaci&oacute;n con sus genes



private void Crossover()
  {
   // Llevamos a cabo el cross over

   // Copiamos los padres, ya que todo el arreglo sera
   // llenado nuevamente con hijos

   Flores PadreA=new Flores();
   Flores PadreB=new Flores();

   // Copiamos los padres
   for(int n=0;n&lt;6;n&#43;&#43;)
   {
    PadreA.cromosoma[n]=poblacion[iPadreA].cromosoma[n];
    PadreB.cromosoma[n]=poblacion[iPadreB].cromosoma[n];

   }

   // Creamos la siguiente generacion
   
   Random random=new Random(unchecked((int)DateTime.Now.Ticks));
   

   for(int n=0;n&lt;10;n&#43;&#43;)
   {
   
    int desde=random.Next(0,5);
    int hasta=random.Next(desde,6);

    for(int c=desde;c&lt;hasta;c&#43;&#43;)
    {
     // Si el random es 0, se copia el gen de PadreA
     // si el random es 1, se copia el gen de PadreB
     if(random.Next(0,2)==0)
      poblacion[n].cromosoma[c]=PadreA.cromosoma[c];
     else
      poblacion[n].cromosoma[c]=PadreB.cromosoma[c];

     // incluimos la mutacion
     if(random.Next(0,100)&lt;=5)
     {

      if(c==0)
       poblacion[n].cromosoma[0]=random.Next(10,300);

      if(c==1)
       poblacion[n].cromosoma[1]=random.Next(0,3);

      if(c==2)
       poblacion[n].cromosoma[2]=random.Next(0,3);

      if(c==3)
       poblacion[n].cromosoma[3]=random.Next(5,15);

      if(c==4)
       poblacion[n].cromosoma[4]=random.Next(20,80);

      if(c==5)
       poblacion[n].cromosoma[5]=random.Next(5,15);

            }

        }
     }
}</pre>
<div class="preview">
<pre class="csharp"><span class="cs__keyword">using</span>&nbsp;System;&nbsp;
&nbsp;
<span class="cs__keyword">namespace</span>&nbsp;AlgoritmosGeneticos&nbsp;
{&nbsp;
&nbsp;<span class="cs__com">///&nbsp;&lt;summary&gt;</span>&nbsp;
&nbsp;<span class="cs__com">///&nbsp;Descripci&oacute;n&nbsp;breve&nbsp;de&nbsp;Flores.</span>&nbsp;
&nbsp;<span class="cs__com">///&nbsp;&lt;/summary&gt;</span>&nbsp;
&nbsp;<span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">class</span>&nbsp;Flores&nbsp;
&nbsp;{&nbsp;
&nbsp;&nbsp;<span class="cs__com">//&nbsp;Variables&nbsp;necesarias&nbsp;para&nbsp;la&nbsp;clase</span>&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">int</span>&nbsp;x;&nbsp;<span class="cs__com">//&nbsp;Posici'on&nbsp;en&nbsp;la&nbsp;ventana</span>&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">double</span>&nbsp;adaptacion;&nbsp;<span class="cs__com">//&nbsp;Nivel&nbsp;de&nbsp;adaptacion&nbsp;del&nbsp;organismo</span>&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;
&nbsp;&nbsp;<span class="cs__com">//&nbsp;Creamos&nbsp;el&nbsp;cromosoma&nbsp;de&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;&nbsp;<span class="cs__com">//&nbsp;0-Altura</span>&nbsp;
&nbsp;&nbsp;<span class="cs__com">//&nbsp;1-Color&nbsp;de&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;&nbsp;<span class="cs__com">//&nbsp;2-Color&nbsp;del&nbsp;tallo</span>&nbsp;
&nbsp;&nbsp;<span class="cs__com">//&nbsp;3-Ancho&nbsp;del&nbsp;tallo</span>&nbsp;
&nbsp;&nbsp;<span class="cs__com">//&nbsp;4-Tama&ntilde;o&nbsp;de&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;&nbsp;<span class="cs__com">//&nbsp;5-Tama&ntilde;o&nbsp;del&nbsp;centro&nbsp;de&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">int</span>[]&nbsp;cromosoma=<span class="cs__keyword">new</span>&nbsp;<span class="cs__keyword">int</span>[<span class="cs__number">6</span>];&nbsp;
&nbsp;
&nbsp;&nbsp;<span class="cs__com">//&nbsp;Creamos&nbsp;las&nbsp;propiedades</span>&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">int</span>&nbsp;CoordX&nbsp;
&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">set</span>&nbsp;{x=<span class="cs__keyword">value</span>;}&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">get</span>&nbsp;{<span class="cs__keyword">return</span>&nbsp;x;}&nbsp;
&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;<span class="cs__keyword">double</span>&nbsp;Adaptacion&nbsp;
&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">set</span>&nbsp;{adaptacion=<span class="cs__keyword">value</span>;}&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">get</span>&nbsp;{<span class="cs__keyword">return</span>&nbsp;adaptacion;}&nbsp;
&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;Flores()&nbsp;
&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;TODO:&nbsp;agregar&nbsp;aqu&iacute;&nbsp;la&nbsp;l&oacute;gica&nbsp;del&nbsp;constructor</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//</span>&nbsp;
&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;}&nbsp;
}&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Creamos&nbsp;un&nbsp;objeto&nbsp;de&nbsp;tipo&nbsp;Random,&nbsp;Luego&nbsp;tenemos&nbsp;un&nbsp;ciclo,&nbsp;donde&nbsp;recorreremos&nbsp;todas&nbsp;las&nbsp;flores&nbsp;de&nbsp;nuestra&nbsp;poblaci&oacute;n.&nbsp;Creamos&nbsp;el&nbsp;objeto&nbsp;flor&nbsp;y&nbsp;asignamos&nbsp;la&nbsp;posici&oacute;n&nbsp;donde&nbsp;le&nbsp;corresponde.&nbsp;Procedemos&nbsp;a&nbsp;rellenar&nbsp;el&nbsp;cromosoma.&nbsp;A&nbsp;cada&nbsp;gen&nbsp;del&nbsp;cromosoma,&nbsp;le&nbsp;colocamos&nbsp;un&nbsp;valor&nbsp;aleatorio&nbsp;de&nbsp;acuerdo&nbsp;con&nbsp;el&nbsp;rango&nbsp;que&nbsp;puede&nbsp;tener.&nbsp;As&iacute;&nbsp;iniciamos&nbsp;una&nbsp;poblaci&oacute;n&nbsp;creada&nbsp;al&nbsp;azar,&nbsp;que&nbsp;deber&aacute;&nbsp;evolucionar&nbsp;hacia&nbsp;el&nbsp;tipo&nbsp;de&nbsp;caracter&iacute;sticas&nbsp;seleccionadas&nbsp;por&nbsp;el&nbsp;usuario.&nbsp;Cuando&nbsp;se&nbsp;ejecute&nbsp;la&nbsp;aplicaci&oacute;n,&nbsp;aparecer&aacute;n&nbsp;diez&nbsp;flores&nbsp;diferentes&nbsp;en&nbsp;la&nbsp;ventana.&nbsp;
&nbsp;
&nbsp;
&nbsp;
<span class="cs__com">//&nbsp;Inicializamos&nbsp;los&nbsp;valores&nbsp;de&nbsp;los&nbsp;cromosomas.</span>&nbsp;
&nbsp;
&nbsp;
&nbsp;
<span class="cs__com">//&nbsp;Arreglo&nbsp;de&nbsp;flores</span>&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">public</span>&nbsp;Flores[]&nbsp;poblacion=<span class="cs__keyword">new</span>&nbsp;Flores[<span class="cs__number">10</span>];&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;System.Windows.Forms.Label&nbsp;lblGeneracion;&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">int</span>&nbsp;generacion=<span class="cs__number">0</span>;&nbsp;
&nbsp;&nbsp;<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">int</span>&nbsp;iPadreA,iPadreB;&nbsp;
&nbsp;
&nbsp;
<span class="cs__keyword">public</span>&nbsp;Form1()&nbsp;
&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Necesario&nbsp;para&nbsp;admitir&nbsp;el&nbsp;Dise&ntilde;ador&nbsp;de&nbsp;Windows&nbsp;Forms</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//</span>&nbsp;
&nbsp;&nbsp;&nbsp;InitializeComponent();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;TODO:&nbsp;agregar&nbsp;c&oacute;digo&nbsp;de&nbsp;constructor&nbsp;despu&eacute;s&nbsp;de&nbsp;llamar&nbsp;a&nbsp;InitializeComponent</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;Random&nbsp;random=<span class="cs__keyword">new</span>&nbsp;Random(<span class="cs__keyword">unchecked</span>((<span class="cs__keyword">int</span>)DateTime.Now.Ticks));&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">for</span>(<span class="cs__keyword">int</span>&nbsp;n=<span class="cs__number">0</span>;n&lt;<span class="cs__number">10</span>;n&#43;&#43;)&nbsp;
&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Flores&nbsp;temp=<span class="cs__keyword">new</span>&nbsp;Flores();&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n]=temp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].CoordX=n*<span class="cs__number">80</span><span class="cs__number">&#43;40</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Inicializamos&nbsp;el&nbsp;cromosoma&nbsp;con&nbsp;valores&nbsp;al&nbsp;azar</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;La&nbsp;altura&nbsp;va&nbsp;de&nbsp;10&nbsp;a&nbsp;300</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">0</span>]=random.Next(<span class="cs__number">10</span>,<span class="cs__number">300</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;El&nbsp;color&nbsp;de&nbsp;la&nbsp;flor.&nbsp;0-rojo,&nbsp;1-azul,&nbsp;2-amarillo</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">1</span>]=random.Next(<span class="cs__number">0</span>,<span class="cs__number">3</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;El&nbsp;color&nbsp;del&nbsp;tallo.&nbsp;Diferentes&nbsp;tonos&nbsp;de&nbsp;verde</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">2</span>]=random.Next(<span class="cs__number">0</span>,<span class="cs__number">3</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;El&nbsp;ancho&nbsp;del&nbsp;tallo.&nbsp;De&nbsp;5&nbsp;a&nbsp;15</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">3</span>]=random.Next(<span class="cs__number">5</span>,<span class="cs__number">15</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;El&nbsp;tamano&nbsp;de&nbsp;la&nbsp;flor.&nbsp;De&nbsp;20&nbsp;a&nbsp;80</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">4</span>]=random.Next(<span class="cs__number">20</span>,<span class="cs__number">80</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;El&nbsp;tamano&nbsp;del&nbsp;centro&nbsp;de&nbsp;la&nbsp;flor.&nbsp;De&nbsp;5&nbsp;a&nbsp;15</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">5</span>]=random.Next(<span class="cs__number">5</span>,<span class="cs__number">15</span>);&nbsp;
&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;
Primero&nbsp;pintamos&nbsp;el&nbsp;suelo.&nbsp;Luego&nbsp;con&nbsp;un&nbsp;ciclo&nbsp;recorremos&nbsp;todas&nbsp;la&nbsp;flores,&nbsp;pintando&nbsp;una&nbsp;por&nbsp;una&nbsp;seg&uacute;n&nbsp;sus&nbsp;caracter&iacute;sticas.&nbsp;Se&nbsp;`pinta&nbsp;el&nbsp;tallo,&nbsp;dependiendo&nbsp;de&nbsp;su&nbsp;color.&nbsp;El&nbsp;color&nbsp;se&nbsp;guarda&nbsp;en&nbsp;el&nbsp;tercer&nbsp;gen,&nbsp;es&nbsp;decir&nbsp;el&nbsp;que&nbsp;se&nbsp;encuentra&nbsp;en&nbsp;el&nbsp;&iacute;ndice&nbsp;<span class="cs__number">2</span>.&nbsp;Al&nbsp;usar&nbsp;el&nbsp;gen&nbsp;en&nbsp;el&nbsp;&iacute;ndice&nbsp;<span class="cs__number">0</span>,&nbsp;vemos&nbsp;su&nbsp;altura,&nbsp;y&nbsp;el&nbsp;valor&nbsp;del&nbsp;gen&nbsp;con&nbsp;&iacute;ndice&nbsp;<span class="cs__number">3</span>&nbsp;nos&nbsp;sirve&nbsp;para&nbsp;colocar&nbsp;el&nbsp;ancho&nbsp;del&nbsp;tallo.&nbsp;
&nbsp;
Para&nbsp;pintar&nbsp;la&nbsp;flor,&nbsp;utilizamos&nbsp;el&nbsp;circulo.&nbsp;Llevamos&nbsp;a&nbsp;cabo&nbsp;la&nbsp;selecci&oacute;n&nbsp;del&nbsp;color&nbsp;usando&nbsp;el&nbsp;el&nbsp;valor&nbsp;contenido&nbsp;en&nbsp;el&nbsp;gen&nbsp;<span class="cs__number">1</span>.&nbsp;Con&nbsp;el&nbsp;valor&nbsp;del&nbsp;gen&nbsp;con&nbsp;&iacute;ndice&nbsp;<span class="cs__number">4</span>,&nbsp;colocamos&nbsp;el&nbsp;tama&ntilde;o.,&nbsp;Todos&nbsp;los&nbsp;centros&nbsp;de&nbsp;las&nbsp;flores&nbsp;se&nbsp;pintan&nbsp;del&nbsp;mismo&nbsp;color,&nbsp;en&nbsp;esta&nbsp;caso,&nbsp;un&nbsp;tono&nbsp;naranja&nbsp;oscuro.&nbsp;El&nbsp;tama&ntilde;o&nbsp;del&nbsp;centro&nbsp;lo&nbsp;obtenemos&nbsp;en&nbsp;el&nbsp;gen&nbsp;con&nbsp;&iacute;ndice&nbsp;<span class="cs__number">5</span>.&nbsp;Despu&eacute;s&nbsp;de&nbsp;pintar&nbsp;todas&nbsp;las&nbsp;flores,&nbsp;actualizamos&nbsp;la&nbsp;etiqueta&nbsp;colocando&nbsp;el&nbsp;valor&nbsp;actual&nbsp;de&nbsp;la&nbsp;generaci&oacute;n.&nbsp;
&nbsp;
&nbsp;
<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Form1_Paint(<span class="cs__keyword">object</span>&nbsp;sender,&nbsp;System.Windows.Forms.PaintEventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Pintamos&nbsp;un&nbsp;suelo</span>&nbsp;
&nbsp;&nbsp;&nbsp;e.Graphics.FillRectangle(Brushes.DarkGreen,<span class="cs__number">0</span>,<span class="cs__number">550</span>,<span class="cs__number">800</span>,<span class="cs__number">50</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Pintamos&nbsp;las&nbsp;flores</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">for</span>(<span class="cs__keyword">int</span>&nbsp;n=<span class="cs__number">0</span>;n&lt;<span class="cs__number">10</span>;n&#43;&#43;)&nbsp;
&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;0-Altura</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;1-Color&nbsp;de&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;2-Color&nbsp;del&nbsp;tallo</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;3-Ancho&nbsp;del&nbsp;tallo</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;4-Tama&ntilde;o&nbsp;de&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;5-Tama&ntilde;o&nbsp;del&nbsp;centro&nbsp;de&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;pintamos&nbsp;el&nbsp;tallo</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;vemos&nbsp;el&nbsp;color&nbsp;del&nbsp;tallo</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(poblacion[n].cromosoma[<span class="cs__number">2</span>]==<span class="cs__number">0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e.Graphics.FillRectangle(Brushes.DarkGreen,&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].CoordX,<span class="cs__number">550</span>-poblacion[n].cromosoma[<span class="cs__number">0</span>],&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">3</span>],poblacion[n].cromosoma[<span class="cs__number">0</span>]);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(poblacion[n].cromosoma[<span class="cs__number">2</span>]==<span class="cs__number">1</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e.Graphics.FillRectangle(Brushes.Green,&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].CoordX,<span class="cs__number">550</span>-poblacion[n].cromosoma[<span class="cs__number">0</span>],&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">3</span>],poblacion[n].cromosoma[<span class="cs__number">0</span>]);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(poblacion[n].cromosoma[<span class="cs__number">2</span>]==<span class="cs__number">2</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;e.Graphics.FillRectangle(Brushes.LightGreen,&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].CoordX,<span class="cs__number">550</span>-poblacion[n].cromosoma[<span class="cs__number">0</span>],&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">3</span>],poblacion[n].cromosoma[<span class="cs__number">0</span>]);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Pintamos&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//Color&nbsp;cflor=new&nbsp;Color();</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;Color&nbsp;cflor=<span class="cs__keyword">new</span>&nbsp;Color();&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(poblacion[n].cromosoma[<span class="cs__number">1</span>]==<span class="cs__number">0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cflor=Color.Red;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(poblacion[n].cromosoma[<span class="cs__number">1</span>]==<span class="cs__number">1</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cflor=Color.Blue;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(poblacion[n].cromosoma[<span class="cs__number">1</span>]==<span class="cs__number">2</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;cflor=Color.Yellow;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;e.Graphics.FillEllipse(<span class="cs__keyword">new</span>&nbsp;SolidBrush(cflor),&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].CoordX&#43;poblacion[n].cromosoma[<span class="cs__number">3</span>]/<span class="cs__number">2</span>-poblacion[n].cromosoma[<span class="cs__number">4</span>]/<span class="cs__number">2</span>,&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__number">550</span>-poblacion[n].cromosoma[<span class="cs__number">0</span>]-poblacion[n].cromosoma[<span class="cs__number">4</span>]/<span class="cs__number">2</span>,&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">4</span>],poblacion[n].cromosoma[<span class="cs__number">4</span>]);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//Pintamos&nbsp;el&nbsp;centro&nbsp;de&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;e.Graphics.FillEllipse(Brushes.DarkOrange,&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].CoordX&#43;poblacion[n].cromosoma[<span class="cs__number">3</span>]/<span class="cs__number">2</span>-poblacion[n].cromosoma[<span class="cs__number">5</span>]/<span class="cs__number">2</span>,&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__number">550</span>-poblacion[n].cromosoma[<span class="cs__number">0</span>]-poblacion[n].cromosoma[<span class="cs__number">5</span>]/<span class="cs__number">2</span>,&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">5</span>],poblacion[n].cromosoma[<span class="cs__number">5</span>]);&nbsp;
&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;lblGeneracion.Text=<span class="cs__string">&quot;Generacion:&nbsp;&quot;</span>&#43;generacion.ToString();&nbsp;
&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;
El&nbsp;ciclo&nbsp;en&nbsp;donde&nbsp;se&nbsp;lleva&nbsp;a&nbsp;cabo&nbsp;el&nbsp;proceso&nbsp;de&nbsp;la&nbsp;evoluci&oacute;n&nbsp;se&nbsp;incorpora&nbsp;por&nbsp;medio&nbsp;del&nbsp;Timer.&nbsp;Cada&nbsp;vez&nbsp;que&nbsp;el&nbsp;Timer&nbsp;genere&nbsp;el&nbsp;evento,&nbsp;se&nbsp;realizar&aacute;&nbsp;todo&nbsp;el&nbsp;proceso&nbsp;necesario&nbsp;para&nbsp;crear&nbsp;una&nbsp;nueva&nbsp;generaci&oacute;n.&nbsp;El&nbsp;evento&nbsp;del&nbsp;Timer&nbsp;se&nbsp;llama&nbsp;Tick,&nbsp;y,&nbsp;en&nbsp;su&nbsp;handler,&nbsp;colocamos&nbsp;el&nbsp;siguiente&nbsp;c&oacute;digo:&nbsp;
&nbsp;
<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;timer1_Tick(<span class="cs__keyword">object</span>&nbsp;sender,&nbsp;System.EventArgs&nbsp;e)&nbsp;
&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Calculamos&nbsp;la&nbsp;adaptacion</span>&nbsp;
&nbsp;&nbsp;&nbsp;CalculaAdaptacion();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Seleccionamos&nbsp;a&nbsp;los&nbsp;padres</span>&nbsp;
&nbsp;&nbsp;&nbsp;SeleccionaPadres();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Hacemos&nbsp;el&nbsp;crossover&nbsp;y&nbsp;la&nbsp;mutacion</span>&nbsp;
&nbsp;&nbsp;&nbsp;Crossover();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Acutalizamos&nbsp;la&nbsp;generacion</span>&nbsp;
&nbsp;&nbsp;&nbsp;generacion&#43;&#43;;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Redibujamos&nbsp;la&nbsp;ventana</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">this</span>.Invalidate();&nbsp;
&nbsp;&nbsp;}&nbsp;
&nbsp;
En&nbsp;esa&nbsp;funci&oacute;n&nbsp;se&nbsp;invocar&aacute;n&nbsp;a&nbsp;varias&nbsp;funciones&nbsp;especializadas&nbsp;que&nbsp;nos&nbsp;ayudan&nbsp;con&nbsp;el&nbsp;proceso.&nbsp;La&nbsp;primera&nbsp;funci&oacute;n&nbsp;CalculaAdaptacion()&nbsp;sirve&nbsp;para&nbsp;que&nbsp;se&nbsp;calcule&nbsp;el&nbsp;nivel&nbsp;de&nbsp;adaptaci&oacute;n&nbsp;de&nbsp;cada&nbsp;flor.&nbsp;Luego&nbsp;SeleccionaPadres()&nbsp;obtiene&nbsp;los&nbsp;dos&nbsp;padres&nbsp;que&nbsp;se&nbsp;utilizar&aacute;n&nbsp;para&nbsp;crear&nbsp;la&nbsp;siguiente&nbsp;generaci&oacute;n.&nbsp;La&nbsp;funci&oacute;n&nbsp;de&nbsp;CrossOver()&nbsp;hace&nbsp;el&nbsp;intercambio&nbsp;gen&eacute;tico&nbsp;y&nbsp;se&nbsp;encarga&nbsp;de&nbsp;la&nbsp;mutaci&oacute;n.&nbsp;Despu&eacute;s,&nbsp;se&nbsp;incrementa&nbsp;la&nbsp;variable&nbsp;de&nbsp;generaci&oacute;n&nbsp;y&nbsp;se&nbsp;manda&nbsp;a&nbsp;redibujar&nbsp;la&nbsp;ventana.&nbsp;
&nbsp;
&nbsp;
No&nbsp;existe&nbsp;una&nbsp;f&oacute;rmula&nbsp;para&nbsp;el&nbsp;c&aacute;lculo&nbsp;de&nbsp;la&nbsp;adaptaci&oacute;n,;&nbsp;cada&nbsp;aplicaci&oacute;n&nbsp;tendr&aacute;&nbsp;su&nbsp;propia&nbsp;forma&nbsp;de&nbsp;llevar&nbsp;a&nbsp;cabo&nbsp;ese&nbsp;c&aacute;lculo.&nbsp;A&nbsp;veces,&nbsp;puede&nbsp;ser&nbsp;tan&nbsp;sencillo&nbsp;como&nbsp;una&nbsp;resta;&nbsp;otras,&nbsp;se&nbsp;necesitar&aacute;n&nbsp;mecanismos&nbsp;m&aacute;s&nbsp;complicados.&nbsp;Nuestra&nbsp;funci&oacute;n&nbsp;CalculaAdaptacion()&nbsp;queda&nbsp;de&nbsp;la&nbsp;siguiente&nbsp;manera:&nbsp;
&nbsp;
<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;CalculaAdaptacion()&nbsp;
&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Variables&nbsp;para&nbsp;las&nbsp;opciones&nbsp;del&nbsp;usuario</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;altura,color,tamano;&nbsp;
&nbsp;&nbsp;&nbsp;altura=color=tamano=<span class="cs__number">0</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Variables&nbsp;necesarias&nbsp;para&nbsp;el&nbsp;calculo</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">double</span>&nbsp;Aaltura,Acolor,Atamano;&nbsp;
&nbsp;&nbsp;&nbsp;Aaltura=Acolor=Atamano=<span class="cs__number">0.0</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Obtnemos&nbsp;la&nbsp;altura&nbsp;deseada&nbsp;por&nbsp;el&nbsp;usuario</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(rbBajo.Checked==<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;altura=<span class="cs__number">0</span>;&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(rbMedio.Checked==<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;altura=<span class="cs__number">1</span>;&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(rbAlto.Checked==<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;altura=<span class="cs__number">2</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Obtenemos&nbsp;el&nbsp;color&nbsp;deseado&nbsp;por&nbsp;el&nbsp;usuario</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(rbRojo.Checked==<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;color=<span class="cs__number">0</span>;&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(rbAzul.Checked==<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;color=<span class="cs__number">1</span>;&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(rbAmarillo.Checked==<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;color=<span class="cs__number">2</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Obtenemos&nbsp;el&nbsp;tama&ntilde;o&nbsp;de&nbsp;la&nbsp;flor&nbsp;deseado&nbsp;por&nbsp;el&nbsp;usuario</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(rbPequeno.Checked==<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;tamano=<span class="cs__number">0</span>;&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(rbNormal.Checked==<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;tamano=<span class="cs__number">1</span>;&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(rbGrande.Checked==<span class="cs__keyword">true</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;tamano=<span class="cs__number">2</span>;&nbsp;
&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Recorremos&nbsp;toda&nbsp;la&nbsp;poblaci&oacute;n&nbsp;para&nbsp;encontrar&nbsp;su&nbsp;adaptaci&oacute;n</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">for</span>(<span class="cs__keyword">int</span>&nbsp;n=<span class="cs__number">0</span>;n&lt;<span class="cs__number">10</span>;n&#43;&#43;)&nbsp;
&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Checamos&nbsp;el&nbsp;nivel&nbsp;de&nbsp;adaptaci&oacute;n&nbsp;para&nbsp;la&nbsp;altura</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(altura==<span class="cs__number">0</span>)&nbsp;<span class="cs__com">//&nbsp;rango&nbsp;10&nbsp;a&nbsp;100</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Aaltura=poblacion[n].cromosoma[<span class="cs__number">0</span>]/<span class="cs__number">100</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(altura==<span class="cs__number">1</span>)&nbsp;<span class="cs__com">//&nbsp;rango&nbsp;100&nbsp;a&nbsp;200</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Aaltura=poblacion[n].cromosoma[<span class="cs__number">0</span>]/<span class="cs__number">200</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(altura==<span class="cs__number">2</span>)&nbsp;<span class="cs__com">//&nbsp;rango&nbsp;200&nbsp;a&nbsp;300</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Aaltura=poblacion[n].cromosoma[<span class="cs__number">0</span>]/<span class="cs__number">300</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(Aaltura&gt;<span class="cs__number">1.0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Aaltura=<span class="cs__number">1</span>/Aaltura;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Checamos&nbsp;el&nbsp;nivel&nbsp;de&nbsp;adaptaci&oacute;n&nbsp;del&nbsp;color</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(color==poblacion[n].cromosoma[<span class="cs__number">1</span>])&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Acolor=<span class="cs__number">1.0</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Acolor=<span class="cs__number">0.0</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Checamos&nbsp;el&nbsp;nivel&nbsp;de&nbsp;adaptaci&oacute;n&nbsp;del&nbsp;tama&ntilde;o&nbsp;de&nbsp;la&nbsp;flor</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(tamano==<span class="cs__number">0</span>)&nbsp;<span class="cs__com">//&nbsp;rango&nbsp;20&nbsp;a&nbsp;40</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Atamano=poblacion[n].cromosoma[<span class="cs__number">4</span>]/<span class="cs__number">40</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(tamano==<span class="cs__number">1</span>)&nbsp;<span class="cs__com">//&nbsp;rango&nbsp;40&nbsp;a&nbsp;60</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Atamano=poblacion[n].cromosoma[<span class="cs__number">4</span>]/<span class="cs__number">60</span>;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;<span class="cs__keyword">if</span>(tamano==<span class="cs__number">2</span>)&nbsp;<span class="cs__com">//&nbsp;rango&nbsp;60&nbsp;a&nbsp;80</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Atamano=poblacion[n].cromosoma[<span class="cs__number">4</span>]/<span class="cs__number">80</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(Atamano&gt;<span class="cs__number">1.0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;Atamano=<span class="cs__number">1</span>/Atamano;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Calculamos&nbsp;el&nbsp;valor&nbsp;final&nbsp;de&nbsp;adaptaci&oacute;n</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].Adaptacion=(Aaltura&#43;Acolor&#43;Atamano)/<span class="cs__number">3.0</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;
Para&nbsp;calcular&nbsp;la&nbsp;adaptaci&oacute;n,se&nbsp;calculan&nbsp;tres&nbsp;valores,&nbsp;uno&nbsp;para&nbsp;cada&nbsp;caracter&iacute;stica&nbsp;que&nbsp;queremos&nbsp;comparar&nbsp;y,&nbsp;luego,&nbsp;se&nbsp;saca&nbsp;el&nbsp;promedio&nbsp;entre&nbsp;ellos,&nbsp;Dentro&nbsp;de&nbsp;la&nbsp;funci&oacute;n,&nbsp;en&nbsp;primer&nbsp;lugar,&nbsp;reconocemos&nbsp;cu&aacute;les&nbsp;son&nbsp;las&nbsp;caracter&iacute;sticas&nbsp;que&nbsp;ha&nbsp;solicitado&nbsp;el&nbsp;usuario,&nbsp;mediante&nbsp;la&nbsp;lectura&nbsp;de&nbsp;los&nbsp;Radio&nbsp;Buttons.&nbsp;Luego&nbsp;recorreremos&nbsp;toda&nbsp;la&nbsp;poblaci&oacute;n&nbsp;y&nbsp;calculamos&nbsp;el&nbsp;valor&nbsp;de&nbsp;adaptaci&oacute;n&nbsp;para&nbsp;cada&nbsp;flor.&nbsp;Como&nbsp;podemos&nbsp;ver,&nbsp;cada&nbsp;caracter&iacute;stica&nbsp;tiene&nbsp;su&nbsp;propia&nbsp;forma&nbsp;de&nbsp;calcular&nbsp;su&nbsp;nivel&nbsp;de&nbsp;adaptaci&oacute;n;&nbsp;luego,&nbsp;sacamos&nbsp;el&nbsp;promedio&nbsp;entre&nbsp;ellos&nbsp;
&nbsp;
La&nbsp;funci&oacute;n&nbsp;para&nbsp;la&nbsp;selecci&oacute;n&nbsp;de&nbsp;los&nbsp;padres&nbsp;es&nbsp;SeleccionaPadres().&nbsp;Esta&nbsp;funci&oacute;n&nbsp;resulta&nbsp;muy&nbsp;sencilla,&nbsp;simplemente,&nbsp;selecciona&nbsp;las&nbsp;dos&nbsp;flores&nbsp;con&nbsp;valor&nbsp;valor&nbsp;de&nbsp;adaptaci&oacute;n.&nbsp;Los&nbsp;&iacute;ndices&nbsp;donse&nbsp;se&nbsp;encuentran&nbsp;son&nbsp;guardados&nbsp;en&nbsp;las&nbsp;variables&nbsp;iPadreA&nbsp;e&nbsp;iPadreB.&nbsp;
&nbsp;
<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;SeleccionaPadres()&nbsp;
&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Seleccionamos&nbsp;los&nbsp;dos&nbsp;mejores</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Modelo&nbsp;elitista</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;iPadreA=iPadreB=<span class="cs__number">0</span>;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Encontramos&nbsp;el&nbsp;padre&nbsp;A</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">for</span>(<span class="cs__keyword">int</span>&nbsp;n=<span class="cs__number">0</span>;n&lt;<span class="cs__number">10</span>;n&#43;&#43;)&nbsp;
&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(poblacion[n].Adaptacion&gt;poblacion[iPadreA].Adaptacion)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;iPadreA=n;&nbsp;
&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Encontramos&nbsp;el&nbsp;padre&nbsp;B</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">for</span>(<span class="cs__keyword">int</span>&nbsp;n=<span class="cs__number">0</span>;n&lt;<span class="cs__number">10</span>;n&#43;&#43;)&nbsp;
&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(poblacion[n].Adaptacion&gt;poblacion[iPadreB].Adaptacion&nbsp;&amp;&amp;&nbsp;iPadreA!=n)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;iPadreB=n;&nbsp;
&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;}&nbsp;
&nbsp;
La&nbsp;funci&oacute;n&nbsp;para&nbsp;el&nbsp;cruce&nbsp;de&nbsp;los&nbsp;cromosomas.&nbsp;En&nbsp;la&nbsp;funci&oacute;n&nbsp;CrossOver(),&nbsp;tomamos&nbsp;los&nbsp;padres&nbsp;seleccionados&nbsp;y&nbsp;creamos&nbsp;una&nbsp;nueva&nbsp;generaci&oacute;n&nbsp;con&nbsp;sus&nbsp;genes&nbsp;
&nbsp;
&nbsp;
&nbsp;
<span class="cs__keyword">private</span>&nbsp;<span class="cs__keyword">void</span>&nbsp;Crossover()&nbsp;
&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Llevamos&nbsp;a&nbsp;cabo&nbsp;el&nbsp;cross&nbsp;over</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Copiamos&nbsp;los&nbsp;padres,&nbsp;ya&nbsp;que&nbsp;todo&nbsp;el&nbsp;arreglo&nbsp;sera</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;llenado&nbsp;nuevamente&nbsp;con&nbsp;hijos</span>&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;Flores&nbsp;PadreA=<span class="cs__keyword">new</span>&nbsp;Flores();&nbsp;
&nbsp;&nbsp;&nbsp;Flores&nbsp;PadreB=<span class="cs__keyword">new</span>&nbsp;Flores();&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Copiamos&nbsp;los&nbsp;padres</span>&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">for</span>(<span class="cs__keyword">int</span>&nbsp;n=<span class="cs__number">0</span>;n&lt;<span class="cs__number">6</span>;n&#43;&#43;)&nbsp;
&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;PadreA.cromosoma[n]=poblacion[iPadreA].cromosoma[n];&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;PadreB.cromosoma[n]=poblacion[iPadreB].cromosoma[n];&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Creamos&nbsp;la&nbsp;siguiente&nbsp;generacion</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;Random&nbsp;random=<span class="cs__keyword">new</span>&nbsp;Random(<span class="cs__keyword">unchecked</span>((<span class="cs__keyword">int</span>)DateTime.Now.Ticks));&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;<span class="cs__keyword">for</span>(<span class="cs__keyword">int</span>&nbsp;n=<span class="cs__number">0</span>;n&lt;<span class="cs__number">10</span>;n&#43;&#43;)&nbsp;
&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;desde=random.Next(<span class="cs__number">0</span>,<span class="cs__number">5</span>);&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">int</span>&nbsp;hasta=random.Next(desde,<span class="cs__number">6</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">for</span>(<span class="cs__keyword">int</span>&nbsp;c=desde;c&lt;hasta;c&#43;&#43;)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;Si&nbsp;el&nbsp;random&nbsp;es&nbsp;0,&nbsp;se&nbsp;copia&nbsp;el&nbsp;gen&nbsp;de&nbsp;PadreA</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;si&nbsp;el&nbsp;random&nbsp;es&nbsp;1,&nbsp;se&nbsp;copia&nbsp;el&nbsp;gen&nbsp;de&nbsp;PadreB</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(random.Next(<span class="cs__number">0</span>,<span class="cs__number">2</span>)==<span class="cs__number">0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[c]=PadreA.cromosoma[c];&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">else</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[c]=PadreB.cromosoma[c];&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__com">//&nbsp;incluimos&nbsp;la&nbsp;mutacion</span>&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(random.Next(<span class="cs__number">0</span>,<span class="cs__number">100</span>)&lt;=<span class="cs__number">5</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;{&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(c==<span class="cs__number">0</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">0</span>]=random.Next(<span class="cs__number">10</span>,<span class="cs__number">300</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(c==<span class="cs__number">1</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">1</span>]=random.Next(<span class="cs__number">0</span>,<span class="cs__number">3</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(c==<span class="cs__number">2</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">2</span>]=random.Next(<span class="cs__number">0</span>,<span class="cs__number">3</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(c==<span class="cs__number">3</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">3</span>]=random.Next(<span class="cs__number">5</span>,<span class="cs__number">15</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(c==<span class="cs__number">4</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">4</span>]=random.Next(<span class="cs__number">20</span>,<span class="cs__number">80</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;<span class="cs__keyword">if</span>(c==<span class="cs__number">5</span>)&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;poblacion[n].cromosoma[<span class="cs__number">5</span>]=random.Next(<span class="cs__number">5</span>,<span class="cs__number">15</span>);&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;}&nbsp;
}</pre>
</div>
</div>
</div>
<h1><span>Source Code Files</span></h1>
<p><span><br>
</span></p>
<h1>More Information</h1>
<p><em>For more information on X, see ...?</em></p>