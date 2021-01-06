# My Blog Sample
([English translate](TestingAndBugFixing.md))  

### Test manuali e correzioni di bug noti [backend, frontend, testing]

Giovanni ha chiesto a Tommaso di dare un'occhiata al sito perché sembra ci siano dei problemi.  

Tommaso si è reso conto di aver modificato la UI del progetto Web, ma di non aver sistemato i test *should_retrieve_all_posts*, *should_retrieve_no_one_category* e *should_retrieve_no_one_tag* del progetto *Magicianred.LearnByDoing.MyBlog.Web.Tests.Integration* che ora riportano degli errore.  
Alcuni test del progetto *Magicianred.LearnByDoing.MyBlog.DAL.Tests.Unit.Repositories* falliscono con questo errore: *System.Data.SQLite.SQLiteException : SQL logic error near "OFFSET": syntax error*. E' un errore relativo al database SQLite usato nei test, prova a capire l'errore e risolverlo.  
Inoltre è stato segnalato un errore nel recupero dei post per tag. Sembra che vengano recuperati sempre tutti i post, bisogna verificare e risolvere il problema.  
Tommaso ti ha chiesto inoltre di dargli una mano per vericare l'esistenza di altri bug. Se ne trovi qualcuno segnalo su GitHub e, poi se vuoi, dai una mano a risolverlo.  

### Specifiche implementative

Nessuna specifica implementativa. In questa attività bisogna eseguire i test e fissare "in qualche modo" gli errori che vengono segnalati dai test. Se non riesci a trovare la soluzione ad un test passa al successivo. Quando hai provato a risolvere tutti i test passa a vedere le soluzioni nel repository.  

[Vedi il repository con l'implementazione (!!!contiene spoiler)](https://github.com/Magicianred/my-blog-sample/tree/pathFromV1toV2/step05/bug-fixing)  


[Ritorna alla pagina principale](../README_IT.md)  
