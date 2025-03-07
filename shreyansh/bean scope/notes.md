Prototype bean is initialized whenever u hit api
in request scope with proxumode,targetlass when called by singleton scope then u have to craete dummy obhject till actual object is present while making http reuest otherwise u would get an error
application scope-1 object across all IOC

By default reuired is true in @Autowired that object should be present ,u can make it false by @Autowired(required=false)
