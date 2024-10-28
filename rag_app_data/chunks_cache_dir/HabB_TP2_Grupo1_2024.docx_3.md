Page label: 4
File name: HabB_TP2_Grupo1_2024.docx.pdf
text:
Trabajo
Práctico
N°2
Página
:
4
de
8
class
PrepareVectorDB:
def
__init__(self,
doc_dir:
str,
chunk_size:
int,
chunk_overlap:
int,
embedding_model:
str,
vectordb_dir:
str,
collection_name:
str)
->
None:
self.doc_dir
=
doc_dir
self.chunk_size
=
chunk_size
self.chunk_overlap
=
chunk_overlap
self.embedding_model
=
embedding_model
self.vectordb_dir
=
vectordb_dir
self.collection_name
=
collection_name
def
run(self):
if
not
os.path.exists(here(self.vectordb_dir)):
os.makedirs(here(self.vectordb_dir))
print(f"Directory
'{self.vectordb_dir}'
was
created.")
#
Load
documents
and
create
embeddings...
2 . 2 . 1 .C a r g a ryP r o c e s a rD o c u m e n t o s
●Car g adeDocument os:Utiliza
PyPDFLoaderpar acar g ardocument osPDFdesdeundir ect orioespecificado.Estabibliot ecapermit ee xtr aert e xt odear chi v osPDF ,loqueesfundamentalpar apr epar arlosdat ospar aelpr ocesamient o.
●Di visióndeT e xt o:Implementa
RecursiveCharacterTextSplitter,quepermit edi vidirelt e xt oenfr agment osqueseajust enaltamañoysuperposiciónespecificados.Estat écnicaescrucialpar agestionart e xt oslar gosyasegur arquesemant eng aelcont e xt osemánticoencadafr agment o.
2 . 2 . 2 .G e n e r a c i ó nd eE m b e d d i n g s
●Seutilizan
OpenAIEmbeddingspar acon v ertirlosfr agment osdet e xt oenv ect or es.Est osembeddingssonr epr esentacionesmat emáticasdel
Habilitación
Profesional
B
–
2024
Facultad
de
Ing.
y
Tecnología
Informática