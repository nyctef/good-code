Tests in particular should be [DAMP rather than DRY](http://stackoverflow.com/a/11837973/895407).

Be wary of reducing duplication in tests - if you find yourself pulling out lots of dependency boilerplate
into setup methods when testing a class, consider if the class having so many dependencies indicates that it has too many
responsibilities. This is one of the easiest ways to 'listen to the tests.'

Be especially wary of pulling out important test details from the test itself. If you find you have to write something 
like this:

```csharp
[Test] 
public void TestFoo() 
{
  var source = GetSourceTestCase("ZhuLi");
  var target = GetTargetTestCase("Varrick");
  Assert.NotNull(source.DoTheThingTo(target));
}
```

then something is seriously wrong. This test is completely opaque - significant digging is required to find out 
what it actually tests, which will cause problems when it inevitably fails.
