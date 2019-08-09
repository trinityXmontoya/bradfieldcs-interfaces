## Data Models
re: What Goes Around Comes Around by Michael Stonebraker & Joseph M. Hellerstein

_What are some of the tradeoffs between relational, hierarchical and network data models?_

Hierarchical data models only allow *one* parent which means we lose the power of foreign keys and join tables,
leading to duplicated (and therefore difficult to maintain) data. It also has 'existence dependency' meaning the existence of a child record depends
on a parent, ex. with `Supplier`s->`Part`s, this means we cannot have a `Part` without a `Supplier`. Lastly, there
is reduced reusability as business needs change because reorganizing data that is structured in a tree is not straightforward.

Network data models allow 1-to-N relationships so information could be represented as a graph. This allowed more model flexibility than hierarchical data models but came with increased query complexity (rather than traversing a straightforward chain where you always know the parent + child, you have to keep track of every 'set' (path) and record type on the graph that you've followed). There were other tradeoffs; because the data is stored as one giant network, loading the database meant loading all the information at once, and if any data became corrupted you had to fix and reload all of it.

Relational data models were intended to provide the most flexibility for data modeling (all the data was stored in tables and you could represent almost anything) and querying (you were comparing entire sets at a time rather than individual records).

Interesting terms:
- existence dependency
- semantic heterogeneity
- schema first vs schema last
- nice to see a technical breakdown of why XML sucks vs just hearing 'XML sucks' ha

Qs:
- I don't understand physical data independence.
- I've normally heard stored procedures discussed as big no-nos because it's your application (not the database)'s job to perform business-related code and it's a mixing of concerns. This paper is supportive of them. The paper is ~15yrs old but is this true / can we discuss when this is / isn't the case?
- As I read about the classification scheme for application data (rigid structure, rigid structure + text, semi-structured, and text) I agreed with their conclusion that with extra thought most data can be rigidly structured.  Are there any good examples since this paper was released of truly unstructurable data / applications?