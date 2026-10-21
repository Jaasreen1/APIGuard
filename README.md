[README (1).md](https://github.com/user-attachments/files/33786135/README.1.md)
# APIGuard
Browser-based API security analyzer with evidence-based findings and automated tests.
[index.html](https://github.com/user-attachments/files/33786142/index.html)<!DOCTYPE html>
<html lang="es">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<title>Analizador de seguridad de API</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=Bricolage+Grotesque:wght@600;800&family=Public+Sans:wght@400;500;600&display=swap" rel="stylesheet">
<style>
:root{--bg:#eef1f4;--sf:#fff;--ink:#14202b;--mut:#566673;--line:#d3dbe2;--acc:#0f5e6b;--onacc:#fff;--code:#f4f7f9;
--crit:#b3261e;--alto:#c2500c;--medio:#946f00;--bajo:#2a6bb0;--info:#566673;--ok:#1f7a45;
box-sizing:border-box;padding-top:env(safe-area-inset-top,0px);padding-bottom:env(safe-area-inset-bottom,0px);color-scheme:light}
@media (prefers-color-scheme:dark){:root:not([data-theme="light"]){--bg:#10171d;--sf:#18222b;--ink:#e6ecf1;--mut:#9aabb8;--line:#2a3945;--acc:#5cc3d1;--onacc:#06232a;--code:#101a21;
--crit:#ff8a80;--alto:#ffa05c;--medio:#e8c04a;--bajo:#7fb6ee;--info:#9aabb8;--ok:#6fd49a;color-scheme:dark}}
:root[data-theme="dark"]{--bg:#10171d;--sf:#18222b;--ink:#e6ecf1;--mut:#9aabb8;--line:#2a3945;--acc:#5cc3d1;--onacc:#06232a;--code:#101a21;
--crit:#ff8a80;--alto:#ffa05c;--medio:#e8c04a;--bajo:#7fb6ee;--info:#9aabb8;--ok:#6fd49a;color-scheme:dark}
html{scroll-padding-top:env(safe-area-inset-top,0px)}
*{box-sizing:border-box}
body{margin:0;background:var(--bg);color:var(--ink);font:400 16px/1.55 "Public Sans",system-ui,-apple-system,"Segoe UI",sans-serif}
.wrap{max-width:1180px;margin:0 auto;padding:28px 20px 56px}
h1{font:800 clamp(28px,4vw,42px)/1.08 "Bricolage Grotesque","Segoe UI",system-ui,sans-serif;margin:0 0 8px;letter-spacing:-.02em}
h2{font:600 18px/1.2 "Bricolage Grotesque","Segoe UI",system-ui,sans-serif;margin:0 0 12px}
.lead{max-width:66ch;color:var(--mut);margin:0 0 18px}
.priv{margin-bottom:18px;font-size:14px}.priv ul{margin:6px 0 0;padding-left:20px}.priv li{margin:3px 0}
.grid{display:grid;grid-template-columns:minmax(0,5fr) minmax(0,6fr);gap:20px;align-items:start}
@media (max-width:860px){.grid{grid-template-columns:1fr}}
.panel{background:var(--sf);border:1px solid var(--line);border-radius:10px;padding:18px}
label{display:block;font-weight:600;font-size:14px;margin:14px 0 5px}
input[type=text],input[type=number],textarea,select{width:100%;font:14px/1.45 ui-monospace,SFMono-Regular,Menlo,Consolas,monospace;background:var(--code);color:var(--ink);border:1px solid var(--line);border-radius:6px;padding:9px 10px}
textarea{resize:vertical;min-height:100px}
.row{display:grid;grid-template-columns:1fr 100px;gap:10px}
:focus-visible{outline:3px solid var(--acc);outline-offset:2px}
button{font:600 14px "Public Sans",system-ui,sans-serif;border-radius:6px;padding:9px 14px;cursor:pointer;border:1px solid var(--line);background:var(--sf);color:var(--ink)}
button:hover{border-color:var(--acc)}
button.go{background:var(--acc);color:var(--onacc);border-color:var(--acc);padding:11px 20px;font-size:15px}
.tabs{display:flex;gap:8px;margin-bottom:16px}.tabs button[aria-pressed=true]{background:var(--acc);color:var(--onacc);border-color:var(--acc)}
.btns{display:flex;gap:10px;margin-top:18px;flex-wrap:wrap}
.hint{font-size:13px;color:var(--mut);margin:4px 0 0}
.empty{color:var(--mut);padding:18px 4px}
.exec{background:var(--code);border-radius:8px;padding:12px 14px;margin:0 0 14px;font-size:15px}.exec p{margin:4px 0}.exec ol{margin:4px 0;padding-left:22px}
.score{display:flex;gap:10px;flex-wrap:wrap;margin:0 0 12px}
.chip{border:1px solid var(--line);border-radius:8px;padding:8px 12px;min-width:84px}
.chip b{display:block;font:800 24px/1 "Bricolage Grotesque",system-ui,sans-serif}
.chip span{font-size:13px;color:var(--mut)}
.verdict{font-weight:600}
details{border:1px solid var(--line);border-left-width:6px;border-radius:8px;margin-bottom:10px;background:var(--sf)}
details[data-s=Crítico]{border-left-color:var(--crit)}details[data-s=Alto]{border-left-color:var(--alto)}
details[data-s=Medio]{border-left-color:var(--medio)}details[data-s=Bajo]{border-left-color:var(--bajo)}details[data-s=Info]{border-left-color:var(--info)}
summary{cursor:pointer;padding:11px 14px;font-weight:600;display:flex;gap:8px;align-items:baseline;flex-wrap:wrap}
.sev{font-size:13px;color:var(--mut)}
.tag{font-size:12px;font-weight:600;border:1px solid var(--line);border-radius:99px;padding:1px 9px;color:var(--mut)}
.tag.sus{border-style:dashed}.tag.inf{opacity:.8}
.body{padding:0 14px 14px;font-size:15px}.body p{margin:8px 0 2px}.body b{font-size:13px;color:var(--mut);font-weight:600;display:block}
pre{margin:4px 0 0;background:var(--code);border-radius:6px;padding:8px 10px;font:13px/1.45 ui-monospace,Menlo,Consolas,monospace;white-space:pre-wrap;overflow-wrap:anywhere}
.msg{font-size:13px;color:var(--ok);align-self:center}
table{width:100%;border-collapse:collapse;font-size:14px}th,td{text-align:left;padding:7px 8px;border-bottom:1px solid var(--line);vertical-align:top}
.tw{overflow-x:auto}.pass{color:var(--ok);font-weight:600}.fail{color:var(--crit);font-weight:600}.sm{font-size:12px;color:var(--mut)}
@media print{.tabs,.priv,.lead,.btns,#vT,#vA>section:first-child{display:none!important}#vA{display:block}body{background:#fff}details{break-inside:avoid}}
@media (prefers-reduced-motion:reduce){*{scroll-behavior:auto!important}}
</style>
</head>
<body>
<div class="wrap">
<h1>Analizador de seguridad de API</h1>
<p class="lead">Pega la respuesta de una API de prueba. El informe separa lo que se observa de lo que solo es sospecha, y trata gravedad, confianza y estado por separado.</p>
<div class="panel priv"><b>Privacidad y alcance</b>
<ul>
<li>Todo se analiza en tu navegador: no se envía nada a ningún servidor ni se guarda en el navegador.</li>
<li>Claves, tokens y correos se enmascaran siempre, también en el texto copiado y en las exportaciones.</li>
<li>Son datos pegados manualmente, no verificados en vivo. La herramienta no hace peticiones: lo «Sospechoso» hay que comprobarlo en un entorno de prueba.</li>
<li>Cada campo se limita a 50.000 caracteres y todo el contenido se trata como texto, nunca como HTML.</li>
<li>Úsala solo con APIs propias o con autorización.</li>
</ul></div>
<div class="tabs"><button type="button" id="tA" aria-pressed="true">Analizar</button><button type="button" id="tT" aria-pressed="false">Pruebas automáticas</button></div>

<div id="vA" class="grid">
<section class="panel" aria-labelledby="t1">
<h2 id="t1">Respuesta a analizar</h2>
<label for="case" style="margin-top:0">Cargar caso de ejemplo</label>
<select id="case"><option value="">— elegir —</option></select>
<label for="url">URL del endpoint</label>
<input type="text" id="url" autocomplete="off" placeholder="https://api.prueba.local/v1/users/7">
<div class="row">
<div><label for="mth">Método</label><select id="mth"><option>GET</option><option>POST</option><option>PUT</option><option>PATCH</option><option>DELETE</option></select></div>
<div><label for="sts">Estado</label><input type="number" id="sts" value="200" min="100" max="599"></div>
</div>
<label for="auth">¿La petición llevó credenciales?</label>
<select id="auth"><option value="nose">No lo sé (no se evalúa)</option><option value="con">Sí, con token o sesión</option><option value="sin">No, fue anónima</option></select>
<label for="hdr">Cabeceras de la respuesta</label>
<textarea id="hdr" spellcheck="false" autocomplete="off" placeholder="Server: nginx&#10;Content-Type: application/json"></textarea>
<label for="bdy">Cuerpo de la respuesta</label>
<textarea id="bdy" spellcheck="false" autocomplete="off" placeholder='{"id": 7, "name": "Ana"}'></textarea>
<div class="btns"><button type="button" class="go" id="run">Analizar respuesta</button><button type="button" id="clr">Borrar datos</button></div>
</section>
<section class="panel" aria-labelledby="t2" aria-live="polite">
<h2 id="t2">Informe</h2>
<div class="btns" style="margin:0 0 12px" id="xb" hidden><button type="button" id="xc">Copiar texto</button><button type="button" id="xj" hidden>Exportar JSON</button><button type="button" id="xh" hidden>Exportar HTML</button><button type="button" id="xp">Imprimir / guardar PDF</button><span class="msg" id="msg"></span></div>
<div id="out"><p class="empty">Carga un caso o pega tu respuesta y pulsa «Analizar respuesta». El informe se recalcula solo si cambias un campo.</p></div>
</section>
</div>

<section id="vT" class="panel" hidden aria-labelledby="t3">
<h2 id="t3">Pruebas automáticas</h2>
<p class="hint" style="margin:0 0 12px">Cada caso declara hallazgos esperados, observaciones informativas requeridas, hallazgos prohibidos, gravedad máxima, estados y comprobaciones de fuga de secretos. Un hallazgo no esperado cuenta como falsa alarma. Se ejecutan al abrir esta pestaña.</p>
<div class="btns" style="margin:0 0 14px"><button type="button" class="go" id="rt">Ejecutar pruebas</button></div>
<div id="ts"></div><div class="tw" id="tb"></div>
</section>
</div>

<script>
var ORDER=["Crítico","Alto","Medio","Bajo","Info"],MAX=50000;
var AUTHL={con:"Sí, con credenciales",sin:"No, petición anónima",nose:"No indicado (no se evalúa)"};
var CURL='curl -i "{u}" -H "Authorization: Bearer <TOKEN_DE_PRUEBA>"   # solo en tu entorno de prueba';
// n=nombre, i=impacto, p=lo que demuestra, np=lo que NO demuestra, c=contexto que cambiaría la evaluación, r=cómo comprobar, f=corrección, v=prueba posterior
var RULES={
HTTP_PLANO:{n:"API consultada por HTTP sin cifrar",i:"Quien esté en la red puede leer o alterar el tráfico.",p:"La URL usa http:// en un host que no es local.",np:"No demuestra que se transmitan credenciales ni que no haya redirección a HTTPS.",c:"Baja si el servidor redirige a HTTPS antes de enviar datos.",r:'curl -I "{u}"   # ¿301/308 hacia https://?',f:"Servir solo HTTPS y redirigir o rechazar HTTP.",v:"La petición HTTP redirige a HTTPS o es rechazada."},
CRED_URL:{n:"Posible credencial en la URL",i:"Las URL quedan en logs, historial y cabeceras Referer.",p:"Un parámetro con nombre de credencial viaja en la URL con un valor que no parece de relleno.",np:"No demuestra que el valor sea una credencial válida.",c:"Desaparece si el valor es un identificador público.",r:"Busca ese parámetro en los logs de acceso de tu entorno de prueba.",f:"Enviar credenciales en la cabecera Authorization.",v:"Con la credencial en la query responde 401; en la cabecera, 200."},
SECRETO:{n:"Clave con formato de secreto real",i:"Una clave activa permite actuar en nombre de su dueño.",p:"El texto coincide con el formato de una clave de nube, pagos o Git.",np:"No demuestra que la clave esté activa ni que sea de producción.",c:"Crítico solo si la clave sigue activa; baja si ya está revocada.",r:"No la uses: revisa en el panel del proveedor si existe y cuándo se usó.",f:"Revocar y rotar la clave; guardarla en un gestor de secretos.",v:"La clave antigua falla y las respuestas ya no contienen el patrón."},
CAMPO_SENS:{n:"Campos con nombre y valor de aspecto secreto",i:"Si son reales, exponen credenciales o datos que el cliente no necesita.",p:"Existe un campo con ese nombre y un valor que no es de relleno.",np:"No demuestra que el valor sea una contraseña o clave válida ni que pertenezca a otra persona.",c:"Cambia si el valor es de prueba o si es el propio dato del solicitante.",r:"Compara los campos devueltos con los que la documentación dice que necesita el cliente.",f:"Devolver solo los campos necesarios (lista blanca / DTO).",v:"Esos campos ya no aparecen en la respuesta."},
JWT_NONE:{n:"Token JWT sin firma (alg none)",i:"Un token sin firma puede ser fabricado por cualquiera.",p:"La cabecera de un token emitido declara alg=none.",np:"No demuestra que otros endpoints acepten ese token.",c:"Empeora si un endpoint protegido lo acepta.",r:"En tu entorno de prueba envía el token a un endpoint protegido y mira si responde 200.",f:"Rechazar alg none y fijar los algoritmos permitidos.",v:"Un token sin firma recibe 401."},
JWT_BODY:{n:"Token JWT en un endpoint que no es de autenticación",i:"Un token expuesto puede reutilizarse para suplantar al usuario.",p:"Hay un JWT en el cuerpo.",np:"No demuestra que esté vigente ni que pertenezca a otro usuario.",c:"Desaparece si es el token del propio solicitante y es el flujo esperado.",r:"Decodifica solo cabecera y payload (sin usarlo) y revisa exp y sub.",f:"No devolver tokens fuera del login; caducidad corta.",v:"La respuesta ya no contiene el token."},
TRAZA:{n:"Error con traza o ruta interna",i:"Revela consultas, archivos y estructura del servidor.",p:"El cuerpo contiene texto de traza, SQL o rutas de archivo.",np:"No demuestra que sea explotable ni que ocurra en producción.",c:"Menor si solo ocurre en desarrollo.",r:"Provoca el mismo error en tu entorno de prueba y compara con producción.",f:"Mensajes genéricos con ID de seguimiento; el detalle solo en logs.",v:"El error devuelve un mensaje genérico sin rutas, SQL ni trazas."},
IP:{n:"IP interna expuesta",i:"Muestra parte de la red interna.",p:"El cuerpo contiene una dirección privada.",np:"No demuestra que sea alcanzable desde fuera.",c:"Depende de si pertenece a tu infraestructura.",r:"Busca la IP en tu inventario de red.",f:"No incluir IPs ni hosts internos.",v:"La respuesta ya no incluye direcciones privadas."},
DEBUG:{n:"Información de depuración en la respuesta",i:"Datos como SQL o entorno ayudan a preparar otros ataques.",p:"Hay campos o cabeceras típicos de depuración con valor activo.",np:"No demuestra que el entorno sea producción.",c:"Menor si es un entorno local de desarrollo.",r:"Revisa si el modo debug está activo en la configuración de ese entorno.",f:"Desactivar el modo debug en producción.",v:"Esos campos ya no aparecen."},
PII:{n:"Datos personales presentes (observación)",i:"Pueden ser necesarios o no según el endpoint.",p:"Hay correos o cédulas en el cuerpo.",np:"No demuestra que sean innecesarios ni que el solicitante no deba verlos.",c:"Se vuelve hallazgo si pertenecen a terceros sin autorización.",r:"Compara los campos con los que usa la aplicación cliente.",f:"Minimizar o enmascarar lo que no se necesite.",v:"La respuesta solo incluye datos necesarios."},
COOKIE:{n:"Cookie sin atributos de protección",i:"Más fácil de robar o de usar en ataques CSRF.",p:"El Set-Cookie no incluye algún atributo Secure, HttpOnly o SameSite.",np:"No demuestra que la cookie guarde la sesión.",c:"Más grave si es la cookie de sesión.",r:'curl -i "{u}"   # revisa las líneas Set-Cookie',f:"Añadir Secure; HttpOnly; SameSite=Strict (o Lax).",v:"Set-Cookie incluye los tres atributos."},
CORS:{n:"CORS permisivo con datos que parecen privados",i:"Otros sitios podrían leer la respuesta desde el navegador del usuario.",p:"Access-Control-Allow-Origin es abierto (*, null) y la respuesta trae campos de aspecto secreto o una combinación inválida.",np:"No demuestra que los datos sean privados ni que el navegador envíe credenciales.",c:"Se descarta si la API es pública y los datos también.",r:'curl -i "{u}" -H "Origin: https://sitio-de-prueba.test"',f:"Usar una lista explícita de orígenes de confianza.",v:"Un origen no autorizado no recibe Access-Control-Allow-Origin."},
HDRS:{n:"Cabeceras de seguridad ausentes",i:"Reducen el daño si algo más falla.",p:"No aparecen en las cabeceras pegadas.",np:"No demuestra una vulnerabilidad explotable por sí sola.",c:"En APIs puras algunas son opcionales.",r:'curl -I "{u}"',f:"Añadir las cabeceras listadas.",v:"curl -I muestra todas las cabeceras."},
VERSION:{n:"Versión de software visible",i:"Facilita buscar vulnerabilidades conocidas.",p:"Una cabecera muestra producto y versión.",np:"No demuestra que esa versión sea vulnerable.",c:"Depende de si está desactualizada.",r:'curl -I "{u}"',f:"Ocultar versiones y mantener el software al día.",v:"La cabecera ya no muestra versiones."},
CACHE:{n:"Datos de aspecto privado posiblemente cacheables",i:"Una caché compartida podría guardar la respuesta.",p:"Hay datos de aspecto privado y Cache-Control no incluye no-store ni private.",np:"No demuestra que exista una caché compartida.",c:"Se descarta si no hay proxies compartidos.",r:'curl -I "{u}"',f:"Cache-Control: no-store en respuestas privadas.",v:"La respuesta incluye Cache-Control: no-store."},
ANON:{n:"Datos devueltos a una petición anónima",i:"Si el recurso no es público, cualquiera podría leerlo.",p:"Una petición marcada como anónima recibió 2xx con campos de aspecto secreto (o datos personales).",np:"No demuestra que falte autenticación: el recurso puede ser público a propósito.",c:"Se descarta si el endpoint es público por diseño.",r:CURL.replace(' -H "Authorization: Bearer <TOKEN_DE_PRUEBA>"',"")+"   # compara con una petición autenticada",f:"Exigir autenticación y autorización en el servidor.",v:"Sin credenciales responde 401 o 403."},
IDOR:{n:"Identificador numérico (observación)",i:"Solo importa si falta control de propiedad.",p:"El recurso usa un ID numérico.",np:"No demuestra IDOR: eso exige acceder a datos ajenos.",c:"Sube a hallazgo si A obtiene datos de B con 200.",r:"Con dos cuentas de prueba tuyas, pide con el token de A el recurso de B.",f:"Comprobar la propiedad en el servidor; IDs no predecibles como defensa extra.",v:"El token de A pidiendo el recurso de B da 403 o 404."},
ROLE:{n:"Campo de rol visible (observación)",i:"El riesgo es la asignación masiva, no el campo en sí.",p:"La respuesta incluye role, admin o permissions.",np:"No demuestra que se puedan modificar privilegios.",c:"Sube a hallazgo si un PATCH con ese campo es aceptado.",r:"En pruebas, envía un PATCH con el campo desde una cuenta sin privilegios.",f:"Ignorar campos de privilegio en las entradas del cliente.",v:"El PATCH con role se ignora o da 400/403."},
RATE:{n:"No se anuncian límites de peticiones (observación)",i:"Sin límites, el login podría sufrir fuerza bruta.",p:"No hay cabeceras X-RateLimit-* ni Retry-After.",np:"No demuestra que no existan límites.",c:"Sube a hallazgo si ráfagas de prueba nunca reciben 429.",r:"En tu entorno de prueba, envía ráfagas pequeñas y vigila 429.",f:"Aplicar límites por usuario/IP, sobre todo en login.",v:"Al superar el límite llega 429 con Retry-After."},
BODY_INV:{n:"El cuerpo no es JSON válido (observación)",i:"El análisis de campos queda limitado.",p:"JSON.parse falló con el cuerpo pegado.",np:"No demuestra un problema.",c:"Pega el JSON completo si estaba truncado.",r:"Valida el cuerpo con un validador JSON.",f:"—",v:"—"},
HDR_MAL:{n:"Líneas de cabecera no válidas ignoradas (observación)",i:"Pueden ocultar cabeceras reales.",p:"Hay líneas sin formato nombre: valor.",np:"No demuestra un problema del servidor.",c:"Revisa cómo copiaste las cabeceras.",r:"Vuelve a copiar las cabeceras en bruto.",f:"—",v:"—"},
SIZE:{n:"Entrada recortada al límite (observación)",i:"Parte del contenido no se analizó.",p:"Un campo superó los 50.000 caracteres.",np:"No demuestra un problema.",c:"Analiza por partes.",r:"Divide la respuesta.",f:"—",v:"—"},
NOHDR:{n:"No se pegaron cabeceras (observación)",i:"No se revisaron cabeceras.",p:"El campo está vacío.",np:"No demuestra un problema.",c:"Pega las cabeceras para revisarlas.",r:'curl -i "{u}"',f:"—",v:"—"}
};
function esc(s){return String(s).replace(/[&<>"']/g,function(c){return {"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c]});}
function parseHeaders(t){var h={},ck=[],mal=0;t.split(/\r?\n/).forEach(function(l){if(!l.trim())return;var i=l.indexOf(":");if(i<1){mal++;return;}var k=l.slice(0,i).trim().toLowerCase(),v=l.slice(i+1).trim();if(!/^[a-z0-9!#$%&'*+.^_`|~-]+$/.test(k)){mal++;return;}if(k==="set-cookie")ck.push(v);else h[k]=h[k]?h[k]+", "+v:v;});return{h:h,ck:ck,mal:mal};}
function walk(o,p,out,dp){dp=dp||0;if(dp<20&&o&&typeof o==="object"){Object.keys(o).slice(0,500).forEach(function(k){var q=p?p+"."+k:k;out.push({path:q,key:k,val:o[k]});walk(o[k],q,out,dp+1);});}return out;}
function trunc(s){s=String(s);return s.length>100?s.slice(0,97)+"…":s;}
function mask(v){v=String(v);return v.length<=6?"••••":v.slice(0,3)+"••••("+v.length+" car.)";}
function maskEmail(e){return e.charAt(0)+"***"+e.slice(e.indexOf("@"));}
function maskUrl(u){return u.replace(/([?&][^=&]*=)([^&]*)/g,function(m,a,b){return a+mask(b)});}
var PH=/^(no[-_ ]?configurad[oa]|not[-_ ]?set|change[-_ ]?me|example|ejemplo|test|prueba|none|null|undefined|n\/a|tbd|todo|redacted|x{3,}|your[-_ ].*|<.*>|\*+|•+|\{\{.*\}\}|\$\{.*\})$/i;
function fake(v){v=String(v).trim();return PH.test(v)||/^[a-z]+([-_ ][a-z]+)+$/i.test(v);}
var SECP=[/AKIA[0-9A-Z]{16}/,/sk_live_[0-9A-Za-z]{8,}/,/-----BEGIN [A-Z ]*PRIVATE KEY-----/,/ghp_[0-9A-Za-z]{20,}/,/xox[bp]-[0-9A-Za-z-]{10,}/];
function analyze(d){
var f=[],trunc0=d.headers.length>MAX||d.body.length>MAX||d.url.length>MAX;
d={url:d.url.slice(0,MAX),method:d.method,status:d.status,auth:d.auth,headers:d.headers.slice(0,MAX),body:d.body.slice(0,MAX)};
var H=parseHeaders(d.headers),h=H.h,hasH=Object.keys(h).length>0,b=d.body.trim(),url=d.url.trim(),json=null;
try{json=JSON.parse(b);}catch(e){}
var items=json!==null?walk(json,"",[]):[],path=url.split("?")[0],q=url.indexOf("?")>-1?url.slice(url.indexOf("?")):"";
var authEp=/\/(login|signin|auth|oauth|token|session)/i.test(path),ok2=d.status>=200&&d.status<300;
function add(id,sev,est,conf,ev,why){f.push({id:id,sev:sev,est:est,conf:conf,ev:ev||"—",why:why||"",r:RULES[id]});}
function obs(id,conf,ev){add(id,"Info","Informativo",conf||"Baja",ev,"Observación: no se presenta como problema.");}
if(trunc0)obs("SIZE","Alta","Límite: "+MAX+" caracteres por campo");
if(/^http:\/\//i.test(url)&&!/^http:\/\/(localhost|127\.|\[::1\])/i.test(url))add("HTTP_PLANO","Alto","Confirmado","Alta",path,"El esquema http:// se observa directamente; el impacto es alto porque expone todo el tráfico.");
var cm=q.match(/[?&](api[_-]?key|key|token|access_token|password|pwd|secret|auth)=([^&]{0,300})/i);
if(cm&&cm[2]&&!fake(cm[2]))add("CRED_URL","Alto","Sospechoso","Media",cm[1]+"="+mask(cm[2]),"Alto si el valor es una credencial real; no se puede saber desde aquí.");
var sm=null;SECP.forEach(function(p){var m=(b+" "+url).match(p);if(m&&!sm)sm=m[0];});
if(sm)add("SECRETO","Crítico","Sospechoso","Alta","valor: "+mask(sm),"Crítico solo si la clave sigue activa; el formato es muy específico pero la vigencia no se verifica.");
var sens=items.filter(function(it){return /pass|pwd|hash|secret|api[_-]?key|private|cvv|token|salt/i.test(it.key)&&typeof it.val==="string"&&it.val.length>=8&&!fake(it.val)&&!(authEp&&/token/i.test(it.key));});
if(sens.length){var strong=sens.some(function(s){return /pass|hash|secret|private|cvv|salt/i.test(s.key)}),hs=sens.some(function(s){return /^\$2[aby]\$|^[a-f0-9]{32,}$/i.test(s.val)});add("CAMPO_SENS",strong?"Alto":"Medio","Sospechoso",hs?"Alta":"Media",sens.slice(0,10).map(function(s){return s.path+": "+mask(s.val)}).join("\n"),"El nombre y la forma del valor sugieren un secreto; la gravedad depende de si es real y ajeno.");}
var jw=(b+" "+JSON.stringify(h)).match(/eyJ[\w-]{1,2000}\.eyJ[\w-]{1,2000}\.[\w-]{0,2000}/g)||[];
var none=jw.filter(function(t){try{return /^none$/i.test(JSON.parse(atob(t.split(".")[0].replace(/-/g,"+").replace(/_/g,"/"))).alg);}catch(e){return false;}});
if(none.length)add("JWT_NONE","Alto","Confirmado","Alta","alg: none en "+mask(none[0]),"Un servidor que emite tokens sin firma ya es un fallo; la aceptación en otros endpoints no se verifica.");
else if(jw.length&&!authEp)add("JWT_BODY","Medio","Sospechoso","Baja",mask(jw[0]),"Medio si el token es válido y ajeno; el indicio es débil.");
var tr=b.match(/SQLSTATE|ORA-\d{3,5}|Traceback \(most recent|\bat [\w.$<>]{1,100} \(.{1,200}:\d+:\d+\)|NullPointerException|\/(var|home|usr|opt)\/[\w.\/-]{1,200}|[A-Z]:\\[\w\\.-]{1,200}/);
if(tr)add("TRAZA","Alto","Confirmado","Alta",trunc(b.split("\n")[0]),"El texto de traza o ruta se observa directamente; ayuda a un atacante, pero no es una explotación directa.");
var ip=b.match(/\b(10\.\d{1,3}|192\.168|172\.(1[6-9]|2\d|3[01]))\.\d{1,3}\.\d{1,3}\b/);
if(ip)add("IP","Bajo","Confirmado","Alta",ip[0],"La IP se observa directamente; el impacto es bajo por sí solo.");
var dbg=items.filter(function(it){return /^(debug|trace|stacktrace|sql|query|env|config|dump)$/i.test(it.key)&&it.val&&it.val!=="false";});
var dh=Object.keys(h).filter(function(k){return /^x-debug/.test(k)});
if(dbg.length||dh.length)add("DEBUG","Medio","Confirmado","Alta",dbg.slice(0,10).map(function(i){return i.path+": "+(typeof i.val==="object"?"{…}":trunc(i.val))}).concat(dh).join("\n"),"Los campos de depuración se observan; el impacto depende del entorno.");
var em=b.match(/[\w.+-]{1,64}@[\w-]{1,63}\.[\w.]{2,32}/g)||[],ce=b.match(/\b\d{3}-\d{7}-\d\b/g)||[],pii=em.length+ce.length>0;
if(pii)obs("PII","Baja",em.slice(0,2).map(maskEmail).concat(ce.slice(0,1).map(mask)).join(", "));
if(d.auth==="sin"&&ok2){if(sens.length)add("ANON","Alto","Sospechoso","Media","HTTP "+d.status+" con credenciales = No; devolvió campos de aspecto secreto","Alto si el endpoint no es público; si lo es, sería un falso positivo.");else if(pii)obs("ANON","Baja","HTTP "+d.status+" anónimo con datos personales");}
H.ck.forEach(function(c){var n=c.split("=")[0].trim(),miss=["Secure","HttpOnly","SameSite"].filter(function(a){return !new RegExp("(^|;)\\s*"+a,"i").test(c)});if(miss.length)add("COOKIE",/sess|sid|auth|token|jwt/i.test(n)?"Medio":"Bajo","Confirmado","Alta",n+": falta "+miss.join(", "),"La falta se observa directamente; la gravedad depende de si es la cookie de sesión.");});
var ao=h["access-control-allow-origin"],ac=h["access-control-allow-credentials"]||"";
if(ao==="null"||(ao==="*"&&(sens.length||/true/i.test(ac))))add("CORS",ao==="*"&&!sens.length?"Bajo":"Medio","Sospechoso","Media","Access-Control-Allow-Origin: "+ao+(ac?"\nAccess-Control-Allow-Credentials: "+ac:""),"Solo se alerta por datos de aspecto secreto o combinación inválida; un * en una API pública es normal.");
if(hasH){var ms=[];if(!h["x-content-type-options"])ms.push("X-Content-Type-Options");if(!h["content-security-policy"])ms.push("Content-Security-Policy");if(!h["x-frame-options"]&&!/frame-ancestors/i.test(h["content-security-policy"]||""))ms.push("X-Frame-Options");if(!h["strict-transport-security"]&&/^https/i.test(url))ms.push("Strict-Transport-Security");if(ms.length)add("HDRS","Bajo","Confirmado","Alta","Ausentes: "+ms.join(", "),"La ausencia se observa; son medidas de endurecimiento.");
["server","x-powered-by","x-aspnet-version"].forEach(function(k){if(h[k]&&/\d/.test(h[k]))add("VERSION","Bajo","Confirmado","Alta",k+": "+h[k],"La versión se observa; el riesgo depende de su antigüedad.");});
if((sens.length||pii)&&!/no-store|private/i.test(h["cache-control"]||""))add("CACHE","Bajo","Sospechoso","Media","Cache-Control: "+(h["cache-control"]||"(ausente)"),"Requiere una caché compartida en el camino.");
if(!Object.keys(h).some(function(k){return /ratelimit|retry-after/.test(k)}))obs("RATE","Baja","Sin X-RateLimit-* ni Retry-After");
}else obs("NOHDR","Baja","—");
if(H.mal)obs("HDR_MAL","Alta",H.mal+" línea(s) ignorada(s)");
if(b&&json===null)obs("BODY_INV","Alta",trunc(b.split("\n")[0]));
var top=Array.isArray(json)?json[0]:json;
if(ok2&&b&&((top&&typeof top==="object"&&typeof top.id==="number")||/\/\d+$/.test(path)))obs("IDOR","Baja",top&&typeof top.id==="number"?"id: "+top.id:path);
if(top&&typeof top==="object"){var rk=Object.keys(top).filter(function(k){return /^(role|roles|is_?admin|admin|permissions)$/i.test(k)});if(rk.length)obs("ROLE","Baja",rk.join(", "));}
var SW={"Crítico":4,"Alto":3,"Medio":2,"Bajo":1,"Info":0},CW={Alta:1,Media:.6,Baja:.3};
function sc(x){return x.est==="Informativo"?-1:SW[x.sev]*CW[x.conf];}
f.sort(function(a,c){return sc(c)-sc(a)||ORDER.indexOf(a.sev)-ORDER.indexOf(c.sev)});
return f;}
function verdict(h){var c=h.filter(function(x){return x.estado==="Confirmado"&&(x.gravedad==="Crítico"||x.gravedad==="Alto")}).length,s=h.filter(function(x){return x.gravedad==="Crítico"||x.gravedad==="Alto"}).length;return c?"Hay problemas confirmados de gravedad alta: corrígelos primero.":s?"No hay problemas altos confirmados, pero sí sospechas de gravedad alta que conviene verificar.":h.length?"Solo hallazgos de gravedad media o baja: planifica su corrección.":"No se encontraron hallazgos con estas comprobaciones. Esto no garantiza que la API sea segura.";}
var LIM=["Análisis estático de datos pegados manualmente: no hace peticiones ni verifica el comportamiento real del servidor.","«Sospechoso» significa que hay indicios por comprobar; no es una vulnerabilidad demostrada.","Los valores secretos aparecen enmascarados en el informe y en las exportaciones.","Cada campo se limita a "+MAX+" caracteres."];
function build(d,f){var u=maskUrl(d.url.trim().slice(0,MAX))||"<URL>",pu=u.split("?")[0];
function ob(x,i){var r=x.r;return{prioridad:i+1,id:x.id,nombre:r.n,gravedad:x.sev,confianza:x.conf,estado:x.est,fragmento:x.ev,demuestra:r.p,no_demuestra:r.np,impacto:r.i,justificacion_gravedad:x.why,contexto_que_cambiaria_la_evaluacion:r.c,como_comprobarlo:r.r.replace("{u}",pu),correccion:r.f,comprobacion_posterior:r.v};}
var hall=f.filter(function(x){return x.est!=="Informativo"}).map(ob),obsv=f.filter(function(x){return x.est==="Informativo"}).map(ob),sv={};
ORDER.slice(0,4).forEach(function(s){sv[s]=hall.filter(function(x){return x.gravedad===s}).length});
return{herramienta:"Analizador de seguridad de API",origen:"Datos pegados manualmente; no verificados en vivo",endpoint:{metodo:d.method,url:u,estado_http:d.status,credenciales:AUTHL[d.auth]},
resumen:{hallazgos:hall.length,confirmados:hall.filter(function(x){return x.estado==="Confirmado"}).length,sospechosos:hall.filter(function(x){return x.estado==="Sospechoso"}).length,observaciones_informativas:obsv.length,por_gravedad:sv,prioridades:hall.slice(0,3).map(function(x){return x.nombre}),veredicto:verdict(hall)},
hallazgos:hall,observaciones:obsv,limites:LIM};}
function toText(o){var L=["INFORME DE SEGURIDAD DE API","Origen: "+o.origen,o.endpoint.metodo+" "+o.endpoint.url+" · HTTP "+o.endpoint.estado_http+" · Credenciales: "+o.endpoint.credenciales,"","RESUMEN EJECUTIVO",o.resumen.veredicto,"Hallazgos: "+o.resumen.hallazgos+" ("+o.resumen.confirmados+" confirmados, "+o.resumen.sospechosos+" sospechosos) · Observaciones: "+o.resumen.observaciones_informativas,""];
function blk(x){return x.prioridad+". "+x.nombre+"\n   Gravedad: "+x.gravedad+" · Confianza: "+x.confianza+" · Estado: "+x.estado+"\n   Fragmento: "+x.fragmento.replace(/\n/g," | ")+"\n   Demuestra: "+x.demuestra+"\n   No demuestra: "+x.no_demuestra+"\n   Impacto: "+x.impacto+"\n   Contexto: "+x.contexto_que_cambiaria_la_evaluacion+"\n   Comprobar: "+x.como_comprobarlo+"\n   Corregir: "+x.correccion+"\n   Verificar: "+x.comprobacion_posterior;}
L.push("HALLAZGOS POR PRIORIDAD");o.hallazgos.forEach(function(x){L.push(blk(x),"")});L.push("OBSERVACIONES INFORMATIVAS (no son hallazgos)");o.observaciones.forEach(function(x){L.push("- "+x.nombre+": "+x.fragmento.replace(/\n/g," | ")+" — no demuestra: "+x.no_demuestra)});L.push("","LÍMITES");o.limites.forEach(function(x){L.push("- "+x)});return L.join("\n");}
function toHTML(o){function blk(x){return '<section class="f"><h3>'+x.prioridad+'. '+esc(x.nombre)+'</h3><p class="t">Gravedad: <b>'+esc(x.gravedad)+'</b> · Confianza: <b>'+esc(x.confianza)+'</b> · Estado: <b>'+esc(x.estado)+'</b></p><dl><dt>Fragmento que lo activó</dt><dd><pre>'+esc(x.fragmento)+'</pre></dd><dt>Demuestra</dt><dd>'+esc(x.demuestra)+'</dd><dt>No demuestra</dt><dd>'+esc(x.no_demuestra)+'</dd><dt>Impacto</dt><dd>'+esc(x.impacto)+'</dd><dt>Gravedad justificada</dt><dd>'+esc(x.justificacion_gravedad)+'</dd><dt>Contexto que cambiaría la evaluación</dt><dd>'+esc(x.contexto_que_cambiaria_la_evaluacion)+'</dd><dt>Cómo comprobarlo (solo en entorno de prueba)</dt><dd><pre>'+esc(x.como_comprobarlo)+'</pre></dd><dt>Corrección</dt><dd>'+esc(x.correccion)+'</dd><dt>Comprobación posterior</dt><dd>'+esc(x.comprobacion_posterior)+'</dd></dl></section>';}
return '<!DOCTYPE html><html lang="es"><head><meta charset="utf-8"><title>Informe de seguridad de API</title><style>body{font:15px/1.5 system-ui,sans-serif;max-width:820px;margin:24px auto;padding:0 16px;color:#14202b}h1{font-size:26px}h3{margin:0 0 4px}.f{border:1px solid #d3dbe2;border-left:6px solid #0f5e6b;border-radius:8px;padding:12px 14px;margin:12px 0;break-inside:avoid}.t{margin:0 0 8px;color:#566673}dt{font-weight:600;font-size:13px;color:#566673;margin-top:8px}dd{margin:2px 0}pre{background:#f4f7f9;padding:8px;border-radius:6px;white-space:pre-wrap;overflow-wrap:anywhere}.b{background:#f4f7f9;padding:10px 14px;border-radius:8px}</style></head><body><h1>Informe de seguridad de API</h1><p>'+esc(o.origen)+'</p><p><code>'+esc(o.endpoint.metodo+" "+o.endpoint.url)+'</code> · HTTP '+esc(o.endpoint.estado_http)+' · Credenciales: '+esc(o.endpoint.credenciales)+'</p><div class="b"><h2>Resumen ejecutivo</h2><p><b>'+esc(o.resumen.veredicto)+'</b></p><p>Hallazgos: '+o.resumen.hallazgos+' ('+o.resumen.confirmados+' confirmados, '+o.resumen.sospechosos+' sospechosos). Observaciones informativas: '+o.resumen.observaciones_informativas+'.</p></div><h2>Hallazgos por prioridad</h2>'+o.hallazgos.map(blk).join("")+'<h2>Observaciones informativas</h2><ul>'+o.observaciones.map(function(x){return '<li><b>'+esc(x.nombre)+'</b>: '+esc(x.fragmento)+' — <i>no demuestra:</i> '+esc(x.no_demuestra)+'</li>'}).join("")+'</ul><h2>Límites</h2><ul>'+o.limites.map(function(x){return '<li>'+esc(x)+'</li>'}).join("")+'</ul></body></html>';}

var SEC0="Content-Type: application/json\nStrict-Transport-Security: max-age=63072000; includeSubDomains\nContent-Security-Policy: default-src 'none'; frame-ancestors 'none'\nX-Content-Type-Options: nosniff\nCache-Control: no-store",SEC=SEC0+"\nX-RateLimit-Limit: 100",J=JSON.stringify,B="https://api.prueba.local";
function C(cat,name,u,st,auth,hd,body,o){o=o||{};return{cat:cat,name:name,expect:o.expect||[],info:o.info||[],forbid:o.forbid||[],max:o.max||"Info",est:o.est||{},evHas:o.evHas||{},noLeak:o.noLeak||[],noRaw:o.noRaw||[],d:{url:u,method:"GET",status:st,auth:auth,headers:hd,body:typeof body==="string"?body:J(body,null,2)}};}
var CASES=[
C("evidente","Credencial en URL, HTTP y secretos","http://api.prueba.local/v1/users/1042?api_key=abc12345",200,"con","Server: Apache/2.4.29 (Ubuntu)\nAccess-Control-Allow-Origin: *\nContent-Type: application/json",{id:1042,name:"Ana",email:"ana@correo.com",password_hash:"$2b$10$Xk3hQ9Lm2",secret_key:"sk_live_51HxAbCdEf12"},{expect:["HTTP_PLANO","CRED_URL","SECRETO","CAMPO_SENS","CORS","HDRS","VERSION","CACHE"],info:["IDOR","PII"],max:"Crítico",est:{HTTP_PLANO:"Confirmado",SECRETO:"Sospechoso"},noLeak:["sk_live_51HxAbCdEf12","$2b$10$Xk3hQ9Lm2","abc12345","ana@correo.com"]}),
C("evidente","Error 500 con traza y rutas",B+"/v1/reports",500,"con",SEC,"Error: SQLSTATE[42000] in /var/www/app/db/Query.php:88\n    at Database.run (/var/www/app/db/index.js:41:13)",{expect:["TRAZA"],max:"Crítico",est:{TRAZA:"Confirmado"}}),
C("evidente","Cookie de sesión sin flags y versión visible",B+"/v1/ping",200,"con",SEC+"\nSet-Cookie: sid=9f8a7b6c; Path=/\nServer: nginx/1.14.0",{ok:true},{expect:["COOKIE","VERSION"],max:"Crítico"}),
C("evidente","JWT firmado con alg none",B+"/v1/auth/login",200,"sin",SEC,{token:"eyJhbGciOiJub25lIn0.eyJzdWIiOiIxIn0."},{expect:["JWT_NONE"],max:"Crítico",est:{JWT_NONE:"Confirmado"}}),
C("evidente","Depuración e IP interna",B+"/v1/orders/list",200,"con",SEC,{debug:true,sql:"SELECT * FROM orders WHERE id=5",host:"10.0.4.17"},{expect:["DEBUG","IP"],max:"Crítico"}),
C("correcta","Perfil con UUID y cabeceras completas",B+"/v1/profile",200,"con",SEC,{id:"b7e1c9d2-41aa-4c0e-9b2f-0d3f6a1e55c1",name:"Ana"},{forbid:["IDOR","ROLE","CORS","ANON"]}),
C("correcta","Estado público sin credenciales",B+"/v1/status",200,"sin",SEC,{status:"ok"},{forbid:["ANON","CORS"]}),
C("correcta","401 correcto sin credenciales",B+"/v1/orders",401,"sin",SEC,{error:"unauthorized"},{forbid:["ANON"]}),
C("correcta","Login legítimo con token HS256",B+"/v1/auth/login",200,"sin",SEC+"\nSet-Cookie: sid=4f9c2a7b; Secure; HttpOnly; SameSite=Strict",{token:"eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJhYmMifQ.c2lnbmF0dXJl",expires_in:3600},{forbid:["CAMPO_SENS","JWT_BODY","JWT_NONE","ANON"],noLeak:["eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJhYmMifQ"]}),
C("correcta","Catálogo público con CORS *",B+"/v1/public/products",200,"sin",SEC+"\nAccess-Control-Allow-Origin: *",[{id:"p1",name:"Libreta",price:120}],{forbid:["CORS","ANON","IDOR"]}),
C("ambigua","ID numérico con autorización",B+"/v1/orders/42",200,"con",SEC,{id:42,total:350},{info:["IDOR"],forbid:["ANON","CAMPO_SENS"]}),
C("ambigua","Directorio con correos, anónimo",B+"/v1/directory",200,"sin",SEC,[{id:"a1",name:"Ana",email:"ana@correo.com"}],{info:["PII","ANON"],forbid:["CORS","CAMPO_SENS"],noLeak:["ana@correo.com"]}),
C("ambigua","Sin cabeceras de límite",B+"/v1/profile",200,"con",SEC0,{id:"u-1",name:"Ana"},{info:["RATE"]}),
C("ambigua","Campo role visible",B+"/v1/profile",200,"con",SEC,{id:"u-1",name:"Ana",role:"viewer"},{info:["ROLE"]}),
C("ambigua","Nombres parecidos a secretos sin valor",B+"/v1/settings",200,"con",SEC,{password_changed:false,token_expires_in:3600,hash_algorithm:"bcrypt",name:"Ana"},{forbid:["CAMPO_SENS"]}),
C("ambigua","Valores de relleno (no-configurado, changeme)",B+"/v1/settings",200,"con",SEC,{token:"no-configurado",api_key:"changeme",password:"********",secret:"not-set"},{forbid:["CAMPO_SENS","JWT_BODY","SECRETO"]}),
C("ambigua","Anónimo con campo de aspecto secreto",B+"/v1/account",200,"sin",SEC,{id:"u1",api_key:"k_9f8a7b6c5d4e"},{expect:["CAMPO_SENS","ANON"],max:"Alto",est:{CAMPO_SENS:"Sospechoso",ANON:"Sospechoso"},noLeak:["k_9f8a7b6c5d4e"]}),
C("robustez","Cabeceras repetidas y mal formadas",B+"/v1/profile",200,"con","Content-Type: application/json\nStrict-Transport-Security: max-age=63072000\nStrict-Transport-Security: max-age=1\nContent-Security-Policy: default-src 'none'; frame-ancestors 'none'\nX-Content-Type-Options: nosniff\nCache-Control: no-store\nX-RateLimit-Limit: 100\nlinea-sin-dos-puntos\n: valor-sin-nombre\nSet-Cookie: a=1; Secure; HttpOnly; SameSite=Lax\nSet-Cookie: lang=es",{id:"u-1"},{expect:["COOKIE"],info:["HDR_MAL"],max:"Bajo"}),
C("robustez","Respuesta vacía (204)",B+"/v1/items/9",204,"con",SEC,"",{forbid:["BODY_INV","IDOR"]}),
C("robustez","JSON inválido",B+"/v1/profile",200,"con",SEC,"{not json",{info:["BODY_INV"]}),
C("robustez","Campo sensible anidado",B+"/v1/me",200,"con",SEC,{user:{profile:{api_key:"k_9f8a7b6c5d4e",name:"Ana"}}},{expect:["CAMPO_SENS"],max:"Medio",evHas:{CAMPO_SENS:"user.profile.api_key"},noLeak:["k_9f8a7b6c5d4e"]}),
C("robustez","Contenido malicioso en cuerpo y cabeceras",B+"/v1/x?q=<scr"+"ipt>alert(1)</scr"+"ipt>",200,"con",SEC+"\nServer: <b>evil</b>/1.0","<img src=x onerror=alert(1)>",{expect:["VERSION"],info:["BODY_INV"],max:"Bajo",noRaw:["<img src=x","<b>evil</b>","<scr"+"ipt>alert"]})
];
function evalTests(){var T={ok:0,n:CASES.length,exp:0,hit:0,miss:0,un:0,forb:0,over:0,est:0,leak:0,rows:[]};
CASES.forEach(function(c,i){var f=analyze(c.d),o=build(c.d,f),hall=f.filter(function(x){return x.est!=="Informativo"}).map(function(x){return x.id}),inf=f.filter(function(x){return x.est==="Informativo"}).map(function(x){return x.id}),all=f.map(function(x){return x.id});
function g(k){return f.filter(function(y){return y.id===k})[0]}
var miss=c.expect.filter(function(e){return hall.indexOf(e)<0}).concat(c.info.filter(function(e){return inf.indexOf(e)<0})),
un=hall.filter(function(e){return c.expect.indexOf(e)<0}),
fb=c.forbid.filter(function(e){return all.indexOf(e)>-1}),
over=f.filter(function(x){return ORDER.indexOf(x.sev)<ORDER.indexOf(c.max)}).map(function(x){return x.id+"="+x.sev}),
est=Object.keys(c.est).filter(function(k){return !g(k)||g(k).est!==c.est[k]}).concat(Object.keys(c.evHas).filter(function(k){return !g(k)||g(k).ev.indexOf(c.evHas[k])<0}).map(function(k){return "ev:"+k})),
html=toHTML(o),ex=J(o)+html+toText(o),
leak=c.noLeak.filter(function(s){return ex.indexOf(s)>-1}).concat(c.noRaw.filter(function(s){return html.indexOf(s)>-1})),
pass=!miss.length&&!un.length&&!fb.length&&!over.length&&!est.length&&!leak.length,n=c.expect.length+c.info.length;
T.exp+=n;T.hit+=n-miss.length;T.miss+=miss.length;T.un+=un.length;T.forb+=fb.length;T.over+=over.length;T.est+=est.length;T.leak+=leak.length;if(pass)T.ok++;
T.rows.push({i:i,c:c,pass:pass,det:[].concat(miss.map(function(x){return "Omitió "+x}),un.map(function(x){return "No esperado "+x}),fb.map(function(x){return "Prohibido "+x}),over.map(function(x){return "Gravedad "+x}),est.map(function(x){return "Estado/evidencia "+x}),leak.map(function(x){return "FUGA "+x.slice(0,12)})),found:all});});
var big=analyze({url:"https://x/y",method:"GET",status:200,auth:"nose",headers:"",body:new Array(300001).join("a")}),sz=big.some(function(x){return x.id==="SIZE"});
T.rows.push({i:-1,c:{cat:"herramienta",name:"Entrada enorme: se recorta y no se bloquea",expect:[],info:["SIZE"],forbid:[],max:"Info"},pass:sz,det:sz?[]:["No avisó del recorte"],found:["SIZE"]});T.n++;if(sz)T.ok++;
return T;}
</script>
<script>
var $=function(i){return document.getElementById(i)},cur=null,ran=false,DL=null;
var SC={"Crítico":"crit","Alto":"alto","Medio":"medio","Bajo":"bajo"};
function data(){return{url:$("url").value,method:$("mth").value,status:parseInt($("sts").value,10)||0,auth:$("auth").value,headers:$("hdr").value,body:$("bdy").value};}
function card(x,open){return '<details data-s="'+esc(x.gravedad)+'"'+(open?" open":"")+'><summary><span class="sev">'+(x.estado==="Informativo"?"Observación":"Prioridad "+x.prioridad)+'</span><span>'+esc(x.nombre)+'</span><span class="tag">Gravedad: '+esc(x.gravedad)+'</span><span class="tag">Confianza: '+esc(x.confianza)+'</span><span class="tag '+(x.estado==="Sospechoso"?"sus":x.estado==="Informativo"?"inf":"")+'">'+esc(x.estado)+'</span></summary><div class="body"><p><b>Fragmento que lo activó</b></p><pre>'+esc(x.fragmento)+'</pre><p><b>Qué demuestra</b>'+esc(x.demuestra)+'</p><p><b>Qué no demuestra</b>'+esc(x.no_demuestra)+'</p><p><b>Impacto</b>'+esc(x.impacto)+'</p><p><b>Gravedad justificada</b>'+esc(x.justificacion_gravedad)+'</p><p><b>Contexto que cambiaría la evaluación</b>'+esc(x.contexto_que_cambiaria_la_evaluacion)+'</p><p><b>Cómo comprobarlo (solo en tu entorno de prueba)</b></p><pre>'+esc(x.como_comprobarlo)+'</pre><p><b>Cómo corregirlo</b>'+esc(x.correccion)+'</p><p><b>Prueba posterior que verifica la corrección</b>'+esc(x.comprobacion_posterior)+'</p></div></details>';}
function render(o){var r=o.resumen,h='<div class="exec"><b>Resumen ejecutivo</b><p class="verdict">'+esc(r.veredicto)+'</p><p>'+esc(o.endpoint.metodo+" "+o.endpoint.url)+' · HTTP '+esc(o.endpoint.estado_http)+' · Credenciales: '+esc(o.endpoint.credenciales)+'</p><p class="sm">Origen: '+esc(o.origen)+'</p>'+(r.prioridades.length?'<p>Corregir primero:</p><ol>'+r.prioridades.map(function(x){return '<li>'+esc(x)+'</li>'}).join("")+'</ol>':'')+'</div><div class="score">'+ORDER.slice(0,4).map(function(s){return '<div class="chip" style="border-left:5px solid var(--'+SC[s]+')"><b>'+r.por_gravedad[s]+'</b><span>'+s+'</span></div>'}).join("")+'<div class="chip"><b>'+r.confirmados+'</b><span>Confirmados</span></div><div class="chip"><b>'+r.sospechosos+'</b><span>Sospechosos</span></div></div>';
h+=o.hallazgos.length?o.hallazgos.map(function(x,i){return card(x,i<2)}).join(""):'<p class="empty">Sin hallazgos con estas comprobaciones.</p>';
if(o.observaciones.length)h+='<h2 style="margin-top:18px">Observaciones informativas</h2><p class="hint" style="margin:0 0 8px">No son hallazgos: indican qué se vio y por qué no basta para afirmar un problema.</p>'+o.observaciones.map(function(x){return card(x,false)}).join("");
$("out").innerHTML=h;$("xb").hidden=false;}
function run(){var d=data();ran=true;if(!d.url.trim()&&!d.headers.trim()&&!d.body.trim()){$("out").innerHTML='<p class="empty">Falta contenido: pega la URL, las cabeceras o el cuerpo, o carga un caso.</p>';$("xb").hidden=true;cur=null;return;}cur=build(d,analyze(d));render(cur);}
function load(i){var d=CASES[i].d;$("url").value=d.url;$("mth").value=d.method;$("sts").value=d.status;$("auth").value=d.auth;$("hdr").value=d.headers;$("bdy").value=d.body;run();}
function say(t){$("msg").textContent=t;setTimeout(function(){$("msg").textContent=""},2500);}
function save(name,txt){if(!cur||!DL)return;DL.save({filename:name,data:txt}).then(function(){say("Guardado")}).catch(function(e){say(e&&e.code==="declined"?"Cancelado":"No se pudo guardar")});}
function tests(){var T=evalTests();
$("ts").innerHTML='<div class="score">'+[[T.ok+"/"+T.n,"Casos correctos"],[T.hit+"/"+T.exp,"Esperados detectados"],[T.miss,"Omitidos"],[T.un,"No esperados"],[T.forb,"Prohibidos presentes"],[T.over,"Gravedad excedida"],[T.est,"Estado/evidencia"],[T.leak,"Fugas"]].map(function(p){return '<div class="chip"><b>'+p[0]+'</b><span>'+p[1]+'</span></div>'}).join("")+'</div>';
$("tb").innerHTML='<table><thead><tr><th>Tipo</th><th>Caso</th><th>Resultado</th><th>Expectativa</th><th>Detalle</th><th></th></tr></thead><tbody>'+T.rows.map(function(r){var c=r.c;return '<tr><td>'+esc(c.cat)+'</td><td>'+esc(c.name)+'</td><td class="'+(r.pass?"pass":"fail")+'">'+(r.pass?"OK":"Falla")+'</td><td class="sm">hallazgos: '+esc(c.expect.join(", ")||"ninguno")+'<br>info: '+esc(c.info.join(", ")||"—")+'<br>prohibidos: '+esc(c.forbid.join(", ")||"—")+'<br>máx: '+esc(c.max)+'</td><td>'+esc(r.det.join(" · ")||"Detectó: "+(r.found.join(", ")||"nada"))+'</td><td>'+(r.i>=0?'<button type="button" data-i="'+r.i+'">Abrir</button>':'')+'</td></tr>'}).join("")+'</tbody></table>';}
function view(t){$("vA").hidden=t;$("vT").hidden=!t;$("tA").setAttribute("aria-pressed",String(!t));$("tT").setAttribute("aria-pressed",String(t));if(t)tests();}
(function(){var s=$("case"),g={};CASES.forEach(function(c,i){if(!g[c.cat]){g[c.cat]=document.createElement("optgroup");g[c.cat].label=c.cat.charAt(0).toUpperCase()+c.cat.slice(1)+"s";s.appendChild(g[c.cat]);}var o=document.createElement("option");o.value=i;o.textContent=c.name;g[c.cat].appendChild(o);});})();
$("case").addEventListener("change",function(){if($("case").value!=="")load(+$("case").value);});
$("run").addEventListener("click",run);
["url","mth","sts","auth","hdr","bdy"].forEach(function(i){$(i).addEventListener("change",function(){if(ran)run();});});
$("clr").addEventListener("click",function(){["url","hdr","bdy"].forEach(function(i){$(i).value=""});$("sts").value=200;$("mth").value="GET";$("auth").value="nose";$("case").value="";cur=null;ran=false;$("xb").hidden=true;$("out").innerHTML='<p class="empty">Datos borrados.</p>';});
$("tA").addEventListener("click",function(){view(false)});$("tT").addEventListener("click",function(){view(true)});$("rt").addEventListener("click",tests);
$("tb").addEventListener("click",function(e){var i=e.target.getAttribute&&e.target.getAttribute("data-i");if(i){view(false);$("case").value=i;load(+i);}});
$("xc").addEventListener("click",function(){if(!cur)return;var t=toText(cur);function fb(){try{var a=document.createElement("textarea");a.value=t;document.body.appendChild(a);a.select();document.execCommand("copy");document.body.removeChild(a);say("Copiado");}catch(e){say("Copia manualmente")}}try{navigator.clipboard.writeText(t).then(function(){say("Copiado")},fb);}catch(e){fb();}});
$("xj").addEventListener("click",function(){save("informe-seguridad-api.json",J(cur,null,2))});
$("xh").addEventListener("click",function(){save("informe-seguridad-api.html",toHTML(cur))});
window.addEventListener("beforeprint",function(){document.querySelectorAll("details").forEach(function(d){d.open=true})});
$("xp").addEventListener("click",function(){try{window.print()}catch(e){say("Usa Exportar HTML e imprime desde el navegador")}});
function blobDL(){return{save:function(o){return new Promise(function(ok){var m=/\.json$/.test(o.filename)?"application/json":"text/html",a=document.createElement("a");a.href=URL.createObjectURL(new Blob([o.data],{type:m+";charset=utf-8"}));a.download=o.filename;document.body.appendChild(a);a.click();document.body.removeChild(a);setTimeout(function(){URL.revokeObjectURL(a.href)},1000);ok();});}};}
function showDL(d){DL=d;$("xj").hidden=false;$("xh").hidden=false;}
try{if(window.claude&&window.claude.use)window.claude.use("downloads").then(function(d){if(d)showDL(d);else showDL(blobDL());}).catch(function(){showDL(blobDL());});else showDL(blobDL());}catch(e){showDL(blobDL());}
</script>
</body>
</html>
