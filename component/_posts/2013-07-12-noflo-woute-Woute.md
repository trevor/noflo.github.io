---
  title: "Woute"
  library: "noflo-woute"
  layout: "component"

---

```coffeescript
EXPORT=SERVER.LISTEN:LISTEN
EXPORT=SPLITROUTES.IN:ROUTES
EXPORT=MERGEROUTES.IN:ROUTE
EXPORT=ROUTER.OUT:OUT

'^(.*)$' -> PATTERN AddCaret(Replace)
'^$1' -> REPLACEMENT AddCaret()
',' -> DELIMITER SplitRoutes(SplitStr) OUT -> IN MergeRoutes(Merge) OUT -> IN AddCaret() OUT -> ROUTE Router(routers/RegexpRouter)

Server(webserver/Server) REQUEST -> IN ParseQuery(webserver/Query) OUT -> IN ParseBody(webserver/BodyParser) OUT -> IN Receiver(woute/Receiver)
Receiver() URL -> IN UrlSplit(Split) OUT -> IN StringifyUrl(woute/StringifyUrl) OUT -> GROUP GroupConnection(groups/Group)

'session-id' -> GROUP SessionId(Group)
Receiver() SID -> IN SessionId() OUT -> IN MergeSections(packets/MergeConnections)
'url' -> GROUP Url(Group)
UrlSplit() OUT -> IN Url() OUT -> IN MergeSections()
'headers' -> GROUP Headers(Group)
Receiver() HEADERS -> IN Headers() OUT -> IN MergeSections()
'query' -> GROUP Query(Group)
Receiver() QUERY -> IN Query() OUT -> IN MergeSections()
'body' -> GROUP Body(Group)
Receiver() BODY -> IN Body() OUT -> IN MergeSections()
'response' -> GROUP Response(Group)
Receiver() RESPONSE -> IN Response() OUT -> IN MergeSections()

MergeSections() OUT -> IN GroupConnection() OUT -> IN Router()

```