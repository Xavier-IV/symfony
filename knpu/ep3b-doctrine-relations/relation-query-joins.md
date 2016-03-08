# Relation Query Joins

Since we’re going to turn this into a proper query for genus note, we’re going
to need a custom query which means we need a genus note repository. So we’ll
copy genus repository to genus note repository, rename that and then clear out
the method and here we’re making new public function find all recent notes for
genus and we’ll have of course a genus argument. Excellent. Now we’re starting
simple here by just return. This arrow create query builder, genus underscore
note. That’s the alias we’re giving our table or entity for this query.

That could be anything, but I usually call that standard and let’s just say get
query, arrow, execute. So right now we’re actually going to return every single
genus note temporarily. Now to wire this up, don’t forget you need to go the
genus note entity and go to at ORM slash entity and add repository class is
genus note repository and then the genus controller, we can just start using
this.

So recent notes equals EM, get repository at bundle colon genus note arrow find
all recent notes for genus and pass the genus object that we queried for a
little bit earlier. So with any luck, temporarily we should be able to flip
over and see that six go to 100 and it does and that’s so awesome except for my
really lame typo on the word recent, embarrassing for me. Let’s fix that. Okay.
Now let’s make our query a little bit more interesting. So this is the first
time we’re querying across relationship and I’m going to show you both sides of
the way you’re doing it and this one is actually pretty easy.

We just want to first add an and where, genus underscore note dot genus is
equal to a particular genus and we’ll fill in colon genus with the genus
object. Now this might seem weird to you. In a database, we would want to query
for genus note where genus underscore ID equals a particular ID, like five, but
remember these are property names. So if we say genus underscore note dot
genus, we can do that because there’s a genus property. So you will query
across the relationship. You use the genus property and then you’ll actually
pass the whole genus object.

Now of course, behind the scenes, doctrine simply converts that into a where
clause for genus underscore ID equals this genus’ ID. So this might look weird
at first, but it’s the same thing that you always do and if you want you can
actually pass the ID as the parameter value instead of the entire object and
then to finish this off, we’ll also add another and where, genus note, dot
created at is greater than colon recent date. No fill on that set parameter
with recent date is new slash date time minus three months. Perfect.

So I’ll head back. Refresh. This should go back to six. It does and the
difference now is it’s making a more efficient query than it was before because
it’s only returning the six note objects to do this and if you wanted to you
can make this query even more efficient by literally returning just the number
six with the count and it’s at least six genus note objects.

It’s all about custom queries in our doctrine queries tutorial. I want to show
you how to query from the other side of the relationship, from genus to genus
note and I want to show you what a join looks like. So here’s the setup. Go to
just slash genus and right now this is ordered by the number of species that
are in each genus. I want to order it by which one has the most recent
activity. So which one has the most recent genus note? So we’re going to order
by a totally different column.

So I’ll close genus note repository and open genus repository and this is the
query that we’re using on that page. Find all published ordered by size. I’m
going to change that to find all published ordered by recently active and I’ll
copy that and go into genus controller and the list, I’ll paste that. I could
have also right clicked on gone to refactor rename and it would change both
instances of that all at once.

So that’s a really good PHP strong trick to use and down here get rid of the
order by and order by genus note dot created at, but you guys how SQL queries
work. We’re only dealing with the genus table here so we can’t automatically
order by that unless we do a left join to it. So say arrow left join genus
because that’s our main table alias dot notes and to join you actually
reference the property on genus that we’re reaching across. So remember this is
the optional inverse side of the relationship that we added and this is a
second reason you would need it.

If you want to do left joins from genus down to genus notes then you need to
have that mapped. The second one I’m going to left join is going to be genus
underscore note. That is the alias that you give this new join table so you can
start using – referencing genus note. So we’ll add order by genus underscore
note dot created at descending and that should be it. Head back. Refresh. And
it’s definitely in a slightly order. If we look at the first one, this one has
something from February 15 which is pretty darn new.

The second one is the latest one is from February 11. So yeah, it looks like it
worked and if we go all the way down to the bottom, this is from December 21
which is pretty long ago. So that’s it. We’re going to know more about querying
cost relationships and all that complicated stuff. We’ll look at our doctrine
queries. One thing to notice is that by default even though we joined across
another table, we are still getting the same result set back.

We’re still getting back an array of genus objects. So the join didn’t affect
the results we got back. It just allowed us to make a more targeted query. All
right, guys. You – there is more to learn about doctrine, but you are really,
really dangerous right now. I hope you absolutely love it. So let’s keep going
and we’re keep going and we’re get on with the symphony series with a totally
different topic. Forms. All right, guys. See you next time.