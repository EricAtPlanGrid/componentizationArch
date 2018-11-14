# Netflix’s Android Componentization Architecture

Lifecycle aware, testable and reusable UI components for Android.

[Droidcon NYC 2018 Talk](https://youtu.be/dS9gho9Rxn4)

Droidcon SF 2018 Talk (Comming Soon)

## Sample code
### Fragment / Activity

~~~kotlin
...
LoadingComponent(container, EventBusFactory.get(this))
...
~~~

### Component (Presenter/Controller/ViewModel)

~~~kotlin
...
bus.getSafeManagedObservable(ScreenStateEvent::class.java)
            .subscribe {
                when (it) {
                    ScreenStateEvent.Loading -> {
                        uiView.show()
                    }
                    ScreenStateEvent.Loaded -> {
                        uiView.hide()
                    }
                    ScreenStateEvent.Error -> {
                        uiView.hide()
                    }
                }
            }
...   
~~~

### UIView

~~~kotlin
class LoadingView(container: ViewGroup) : UIView<UserInteractionEvent>(container) {
    private val view: View =
        LayoutInflater.from(container.context).inflate(R.layout.loading, container, true)
            .findViewById(R.id.loadingSpinner)
...            
~~~

