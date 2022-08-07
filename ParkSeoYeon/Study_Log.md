# 로그인 화면 구현 
```swift
//
//  ViewController.swift
//  SYStudy
//
//  Created by geonhui Yu on 2022/08/07.
//

import UIKit

class ViewController: UIViewController {
    
    private enum Text {
        static var idError: String {
            return "아이디를 확인해주세요"
        }
        static var idSuccess: String {
            return "성공했습니다."
        }
    }
    
    private enum Colors {
        static let error: UIColor = .red
        static let success: UIColor = .blue
    }
    
    @IBOutlet weak var idInputField: UITextField!
    @IBOutlet weak var idLabel: UILabel!
    
    @IBOutlet weak var pwdLabel: UILabel!
    @IBOutlet weak var pwInputField: UITextField!
    
    @IBOutlet weak var resultLabel: UILabel!
    
    @IBAction func pressButton(_ sender: Any) {
        
//        guard let id = idInputField.text, id.count > 0 else {
//            resultLabel.text = "아이디를 입력해주세요"
//            return
//        }
//        guard let pw = pwInputField.text, pw.count > 0 else {
//            resultLabel.text = "비밀번호를 입력해주세요"
//            return
//        }
        
        if isValid {
            
            resultLabel.text = "로그인에 성공했습니다"
            resultLabel.textColor = .blue
            
        } else {
            
            resultLabel.text = "로그인에 실패했습니다"
            resultLabel.textColor = Colors.error
        }
    }
    
    private var isValidId: Bool = false
    private var isValidPwd: Bool = false
    private var isValid: Bool {
        return isValidId && isValidPwd
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
          
        idInputField.delegate = self
        pwInputField.delegate = self
        
        idInputField.placeholder = "Enter your ID"
        idLabel.text = ""
        idLabel.textColor = .red
        
        pwInputField.placeholder = "Enter your Password"
        pwInputField.isSecureTextEntry = true
        pwdLabel.text = ""
        
        resultLabel.text = ""
    }
    
    private func validationId(id: String) -> Bool {
        return id.count > 10 || id.count == 0
    }
    
    private func validationPwd(pwd: String) -> Bool{
        return pwd.count > 10 || pwd.count == 0
    }
}

// MARK: - Delegate
extension ViewController: UITextFieldDelegate {
    
    //처음 선택했을 때
    func textFieldShouldBeginEditing(_ textField: UITextField) -> Bool {
        print("#1", #function)
        return true
    }
    
    //편집모드(키보드)
    func textFieldDidBeginEditing(_ textField: UITextField) {
        print("#2", #function)
    }
    
    //clear할때 태우는거
    func textFieldShouldClear(_ textField: UITextField) -> Bool {
        print("#3", #function)
        
        resultLabel.text = ""
        
        switch textField {
            
        case idInputField:
            isValidId = false
            idLabel.text = ""
            
        case pwInputField:
            isValidPwd = false
            pwdLabel.text = ""
            
        default: break
        }
        
        return true
    }
    
    //enter return
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        print("#4", #function)
        return true
    }
    
    // 입력할 때
    func textField(_ textField: UITextField, shouldChangeCharactersIn range: NSRange, replacementString string: String) -> Bool {
        
        let currentText = NSString(string: textField.text ?? "")
        let finalText = currentText.replacingCharacters(in: range, with: string)
        
        resultLabel.text = ""
        
        switch textField {
        case idInputField:
            
            isValidId = validationId(id: finalText)
            isValidId ? (idLabel.text = "") : (idLabel.text = Text.idError)
            
        case pwInputField:
            
            if validationPwd(pwd: finalText) {
                
                pwdLabel.text = ""
                isValidPwd = true
                
            } else {
                
                pwdLabel.text = "비밀번호를 확인해주세요."
                pwdLabel.textColor = .red
                isValidPwd = false
            }
            
        default: break
        }
        
        return true
    }
}
```
