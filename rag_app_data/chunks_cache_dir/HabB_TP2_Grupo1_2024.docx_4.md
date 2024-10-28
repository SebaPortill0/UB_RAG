Page label: 5
File name: HabB_TP2_Grupo1_2024.docx.pdf
text:
Trabajo
Práctico
N°2
Página
:
5
de
8
cont enidot e xtual,quepermit encompar arlasimilitudentr edif er ent esfr agment os.
●Losv ect or essealmacenanenundir ect oriopersist ent eutilizandoChr omaDB,loqueg ar antizaquelosdat osseanaccesiblespar afutur asconsultasyanálisis.
3 .I m p l e m e n t a c i ó nd eM e m o r i ae nC S V
3 . 1 .D e s c r i p c i ó nd el aM e m o r i ae nC S V
Elenf oquedememoriaenC S Vpermit er egistr arelhist orialdecon v ersacionesconelchat bot .Est emét odoesútilpar aelanálisispost eriorypar amejor arlae xperienciadelusuarioalpr opor cionarunr egistr oestructur adodeint er acciones.Losar chi v osC S Vsonf ácilesdemanipularypermit enlaint egr aciónconherr amientasdeanálisisdedat os.
3 . 2 .C ó d i g od eI m p l e m e n t a c i ó n
Laclase
Memoryseencar g adeescribirelhist orialdecon v ersacionesenunar chi v oC S V :
class
Memory:
@staticmethod
def
write_chat_history_to_file(gradio_chatbot:
List,
thread_id:
str,
folder_path:
str)
->
None:
today_str
=
date.today().strftime('%Y-%m-%d')
#
Prepare
and
write
to
CSV...
3 . 2 . 1 .R e g i s t r od eC o n v e r s a c i o n e s
●Int er ac ciónc onelChat bot:AlmacenaelIDdelhilo,lamar cadetiempo,laconsultadelusuarioylar espuestadelbot .Est opermit equecadaint er acciónser egistr edemaner aúnicayestructur ada.
●Estructur adeAr chi v o:Cadadíasecr eaunnue v oar chi v oC S Vconelf ormat odenombr e
YYYY-MM-DD.csv,asegur andoqueelhist orialsemant eng aor g anizadoyqueseaf ácildeaccederpar aanálisisfutur os.
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