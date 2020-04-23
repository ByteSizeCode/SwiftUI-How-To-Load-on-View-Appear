# SwiftUI-How-To-Load-on-View-Appear
How to load data when a view appears in SwiftUI

The below will NOT work and is not valid SwiftUI. It will give the error on VStack that <span style="color: red"> Type '()' cannot conform to 'View'; only struct/enum/class types can conform to protocols </span>:
```Swift
import SwiftUI

struct ContentView: View {
    @State var value:String = ""
    var body: some View {
        VStack {
            TextField("Nothing typed here", text: $value)
            
            //Fetch date with standard Swift code (non-SwiftUI)
            let date = Date()
            let formatter = DateFormatter()
            formatter.dateFormat = "dd.MM.yyyy"
            let currentDate = formatter.string(from: date)
            
            //Update the data in the view
             self.value = currentDate
             print("Load data")
             print("Updating Text(value)")
            
        }
    }
}
```

Likewise this will NOT work either, as SwiftUI is expecting code for the view (aka SwiftUI syntax):
```Swift
import SwiftUI

struct ContentView: View {
    @State var value:String = ""
    var body: some View {
        VStack {
            TextField("Nothing typed here", text: $value)
            
            LoadDataAndSetIt()
            
        }
    }
    
    func LoadDataAndSetIt() {
      //Fetch date with standard Swift code (non-SwiftUI)
        let date = Date()
        let formatter = DateFormatter()
        formatter.dateFormat = "dd.MM.yyyy"
        let currentDate = formatter.string(from: date)

        //Update the data in the view
        self.value = currentDate
        print("Load data")
        print("Updating Text(value)")
    }
}
```

Instead use the <i>.onAppear</i> property on VStack as follows:

```Swift
import SwiftUI

struct ContentView: View {
    @State var value:String = ""
    var body: some View {
        VStack {
            TextField("Nothing typed here", text: $value)
        }
        .onAppear() {
           //Fetch date with standard Swift code (non-SwiftUI)
            let date = Date()
            let formatter = DateFormatter()
            formatter.dateFormat = "dd.MM.yyyy"
            let currentDate = formatter.string(from: date)
            
            //Update the data in the view
             self.value = currentDate
             print("Load data")
             print("Updating Text(value)")
            
        }
    }
}
```
You have now used standard Swift to load up the current date and update the value in your SwiftUI view
