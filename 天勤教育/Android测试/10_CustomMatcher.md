How to check the colour of Text? How to check the hint of ```EditText``` field?

#### Create Custom Matcher

1. Find out the view you are checking against. e.g. ```TextView, EditText View```.
2. Find the API from which you can get the attributes. ```textView.getCurrentTextColor(); editText.getHint();```.
3. Create custom matcher using ```BoundedMatcher```.



```java
@NonNull
public static Matcher<View> withhintText(final String text) {
    Checks.checkNotNull(text);
    return new BoundedMatcher<View, EditText>(EditText.class) {
        @override
        public boolean matchesSafely(@NonNull EditText editText) {
            return text == editText.getHint().toString();
        }
        @override
        public void describeTo(@NonNull Description description) {
            description.appendText("with edit text: " + text);
        }
    }
}

// Using Custom Matcher
onView(withId(R.id.editTextTest)).check(matches(withHintText("default hint")));
```

From Tutorials Point

https://www.tutorialspoint.com/espresso_testing/espresso_testing_custom_view_matchers.htm

#### Advantages of Custom Matchers

+ To exploit the unique feature of our own custom views.
+ Custom matcher helps in the ```AdapterView``` based test cases to match with the different type of underlying data.
+ To simplify the current matchers by combining features of multiple matcher.

Espresso provides the following two classes to write new matchers:

+ TypeSafeMatcher
+ BoundedMatcher

