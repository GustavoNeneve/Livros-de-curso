$(function (){
  init();
});

function init()
{
// identificar com checkURI qual é a página atual e montar ela.
// caso não exista, procurar no localStorage se existe uma página salva.

    $("#booklet .paginas .pagina").css("display","none");

    if(checkURI("page") == false)
    {
      if(getSavedPage()!= false)
      {
        goTo(getSavedPage(),true);
      }
    }
    pagination();

}

function documentID()
{
  var path = location.pathname + extrairArquivo(location.pathname).arquivo;
  var id = path.hashCode();

      if(id < 0) {
        id *= -1; id = "N" + id.toString();
      }

  if($("html").attr("templateID"))
  {
      id = $("html").attr("templateID");
  }else

  if($("html").attr("id"))
  {
    id = $("html").attr("id");
  }


  return id.toString();
}

// função retirada do site http://werxltd.com/wp/2010/05/13/javascript-implementation-of-javas-string-hashcode-method/
String.prototype.hashCode = function(){
	var hash = 0;
	if (this.length == 0) return hash;
	for (i = 0; i < this.length; i++) {
		char = this.charCodeAt(i);
		hash = ((hash<<5)-hash)+char;
		hash = hash & hash; // Convert to 32bit integer
	}
	return hash;
}

// função retirada do site http://codigofonte.uol.com.br/codigos/extrair-o-nome-do-arquivo-e-a-extensao-com-javascript
function extrairArquivo(Caminho){
	Caminho 	= Caminho.replace("/\/g", "/");
	var Arquivo = Caminho.substring(Caminho.lastIndexOf('/') + 1);
	var Extensao= Arquivo.substring(Arquivo.lastIndexOf('.') + 1);
	return {arquivo:Arquivo, extensao:Extensao};
}

function goTo( i, bool ){
    if(bool){

      var path = location.pathname;
      location.href= extrairArquivo(path).arquivo + "?page=" + i;
    }else{
      var ap = 1;
      if(i <= countPages()){
        ap = i;
      }
      $("#booklet .paginas .pagina").css("display","none");
      $('#booklet').animate({
       scrollTop: 0
   }, 2000);
      $("ul.pagination li").removeClass("active");

      $("ul.pagination li:nth-child(" + ap + ")").addClass("active");
      $("#booklet .paginas .pagina:nth-child(" + ap + ")").css("display", "block");
      savePage(ap);
    }
}

function getSavedPage(){
  var savedPage = false;
  if(localStorage.getItem("savedPage_" + documentID()) != null){
    savedPage = localStorage.getItem("savedPage_" + documentID());
  }
  return savedPage;
}

function savePage( i=null )
{
  var savePage = 1;
      if(i)
      {
        savePage = i;
      }else{
        if(checkURI("page"))
        {
          savePage = checkURI("page");
        }
      }

      localStorage.setItem("savedPage_" + documentID(),savePage);
}

function checkTemp( i )
{
  var saved = false;
  if(localStorage.getItem(i) != null){
    saved = localStorage.getItem(i);
  }
  return saved;
}


function activePage( i )
{

  if(i!=false){
    var ap = 1;
    if(checkURI("page")){
      ap = checkURI("page");
    }
  }else{
    if(i <= countPages()){
      ap = i;
    }
  }

  $("ul.pagination li:nth-child(" + ap + ")").addClass("active");
  $("#booklet .paginas .pagina:nth-child(" + ap + ")").css("display", "block");
  savePage(ap);
}

function pagination ()
{
  $("ul.pagination").css("display","none");
  if(countPages() > 1)
  {
    for(var i = 1; i <= countPages(); i++)
    {
    var li = '<li> <a href="index.html?page=' + i + '" class="btn btn-primary">' + i + '</a> </li>';
      $("ul.pagination").append(li);
    }
    $("ul.pagination").css("display","");
  }else {
    $("ul.pagination").css("display","none !important");
  }

    activePage();
}

function countPages()
{
  var nroPages = $("#booklet .paginas").children().length;
  return nroPages;
}

function checkURI( i )
{
  // var url = location.href;
  var uri = location.search;
  var resp = new Array();
      resp[1] = false;
      if (uri)
      {
          uri = uri.replace("?","");
          while (uri.indexOf("&&")!= -1) {
            uri = uri.replace("&&","&");
          }

      var variaveis = uri.split("&");
          if(variaveis[0] != "")
          {
            for (var p = 0; p <= variaveis.length; p++)
            {
              if(variaveis[p] != undefined){
                var comparar = variaveis[p];
                    comparar = comparar.split("=");
                    if(comparar[0].localeCompare(i) == 0){
                      resp = variaveis[p].split(i + "=");
                      break;
                    }else{
                      resp[1] = false;
                    }
              }
            }
          }else {
            resp[1] = variaveis[0];
          }


      }

      return resp[1];
}



function getIndexFile(){
  var addr_file = location.href;
  if(addr_file.indexOf("index.html") == -1 && addr_file.indexOf("index.htm") == -1) {
    if(addr_file.slide(-1) != "/" ) addr_file += "/";
    addr_file += "index.html";
  }
  return addr_file;
}
