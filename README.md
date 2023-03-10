# swiftui_move_textfield_when_keyboard_shows_up


```swift
struct ContentView: View {
    
    @State var txt = ""
    @State var value: CGFloat = 0
    
    var body: some View {
        VStack {
            List(0..<100) { _ in
                Text("Hello From Paige")
            }
            
            TextField("Type Something", text: self.$txt)
                .textFieldStyle(.roundedBorder)
                .padding(.horizontal, 15)
            
        } //: VSTACK
        .offset(y: -self.value)
        .animation(.spring())
        .onAppear {
            NotificationCenter.default.addObserver(forName: UIResponder.keyboardWillShowNotification, object: nil, queue: .main) { noti in
                let value = noti.userInfo![UIResponder.keyboardFrameEndUserInfoKey] as! CGRect
                let height = value.height
                self.value = height
            }
            
            NotificationCenter.default.addObserver(forName: UIResponder.keyboardWillHideNotification, object: nil, queue: .main) { noti in
                self.value = 0
            }
            
        }
    }
}
```
