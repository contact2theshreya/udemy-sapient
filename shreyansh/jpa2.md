1) Spring boot data jhpa internally provides hibernate dependency so we dont need to externally provide it
2) persistence unit-give configuration like dialect,db connection,driver etc(spp.prop)
3) There can be more than 1 persitence unit can be ptresenr and for each persisrtence unit we have to create entitymanagerfactory(java objevt)
4) enetitymaanager is like session ex if u call save() from jpoa internally it will call enttiymanager.persist
5) entitymsnsgre is interface where we have all query,jpa repo is just wrapper over it but if we want we can create entitymanager also
6) persistent context is placeholder for entity where objects (entity) are stored,it also hepls into first level caching
7) hibernate works with JQL or HQL so dialect translate it to like SQL
8) 

