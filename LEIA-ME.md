FORMATAÇÃO DE MÁSCARA PARA ANDROID STUDIO


Uma biblioteca do Android para formatar as máscaras de uso do Strings. Pode ser usado com o TextWatcher.

A versão mínima do SDK é 7.


Gradle

implementation 'com.github.rtoshiro.mflibrary:mflibrary:1.0.0'
    repositories {
        mavenCentral()
    }
    
Uso Básico

Para formatar e limitar uma entrada EditText, como datas, números de telefone ... você pode usar MaskTextWatcher e SimpleMaskFormatter.

SimpleMaskFormatter vem com 5 padrões pré definidos que você pode usar.

N - para números.
L - para cartas.
L - para números e letras.
l - para letras minúsculas.
U - para letras maiúsculas.

MaskTextWatcher é usado para controlar a entrada de EditText. Então, temos que adicionar o observador em EditText usando o método EditText.addTextChangedListener.

O MaskTextWatcher precisa de dois parâmetros. O primeiro é um TextView (ou EditText como EditText estende TextView) e o segundo é um objeto MaskFormatter.

Exemplo para formatar datas como MM / DD / AAAA:

SimpleMaskFormatter smf = new SimpleMaskFormatter("NN/NN/NNNN");
MaskTextWatcher mtw = new MaskTextWatcher(myEditText, msf)
myEditText.addTextChangedListener(mtw);

OBS.: Em nosso SimpleMaskFormatter, limitamos o uso apenas para números.


Padrões Personalizados

Podemos definir nosso próprio padrão usando o MaskFormatter.

Em nosso exemplo, estamos alterando-o para limitar os números da nossa string de máscara.

Durante meses, vamos limitar o primeiro caractere de 0 a 1 e o segundo caractere de 0 a 9.

Por dia, vamos limitar o primeiro caractere de 0 a 3 e o segundo caractere de 0 a 9.

Precisamos criar 3 objetos MaskPattern:

MaskPattern mp03 = new MaskPattern("[0-3]");
MaskPattern mp09 = new MaskPattern("[0-9]");
MaskPattern mp01 = new MaskPattern("[0-1]");
Then, we need to create a new MaskFormmater:

MaskFormatter mf = new MaskFormatter("[0-1][0-9]/[0-3][0-9]/[0-9][0-9][0-9][0-9]");
And register our patterns in MaskFormatter object:

mf.registerPattern(mp01);
mf.registerPattern(mp03);
mf.registerPattern(mp09);
We can change the pattern representation using our own elements:

MaskFormatter mf = new MaskFormatter("19/39/9999");

mf.registerPattern("1", mp01);
mf.registerPattern("3", mp03);
mf.registerPattern("9", mp09);
