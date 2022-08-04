# CollectionView
- grid Layout을 표현해주는 View이다. (인스타그램 돋보기 모양)
- Section과 Item으로 구분되어 있다. (2개를 묶고 있는 것이 indexPath)
- Flow Layout을 기본으로 사용하며(수평, 수직을 나타내준다.)
- Delegate Pattern을 사용한다.

```swift
extension ColorListViewController: UICollectionViewDataSource {
    
    // MARK: Section이 여러개 존재하는 경우 (기본 값은 1)
    func numberOfSections(in collectionView: UICollectionView) -> Int {
        return list.count // section 수
    }
    
    // MARK: Section에 필요한 Item수
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return list[section].colors.count // item 수
    }
    
    // MARK: cell을 요청한다.
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "cell", for: indexPath)
        
        // itemIndex -> color Data -> Background
        cell.contentView.backgroundColor = list[indexPath.section].colors[indexPath.item]
        return cell
    }
}
```

## FlowLayout이란 
- CollectionView를 수평, 수직으로 나타내 줄 수 있는 뷰 
- ```UICollectionViewFlowLayout```을 따른다.
- Item 사이즈는 기본 50으로 지정된다.
- ```minimumInterItemSpacing```과 ```minimumLineItemSpacing```을 통해 상하좌우 공백을 지정할 수 있다. (기본 값 : 10)
- ```SectionInset```도 적용을 할 수 있다. (기본 값 : 0)
- 위와 같은 속성은 ```UICollectionView```속성이 아닌 Layout의 속성이기 때문에 TypeCating이 필요하다.

```swift
if let layout = listCollectionView.collectionViewLayout as? UICollectionViewFlowLayout { // Type Casting
            
    // MARK: - Cell크기 변경
    layout.itemSize = CGSize(width: 100, height: 100)
            
    // MARK: - Cell 라인 여백, 셀 여백(수직, 수평에 따라 둘이 달라진다.)
    layout.minimumInteritemSpacing = 10
    layout.minimumLineSpacing = 10
           
    // MARK: - Section Inset (항상 같은 값을 유지한다.)
    layout.sectionInset = UIEdgeInsets(top: 40, left: 20, bottom: 20, right: 40)
}
```
## Custom Cell 
- 기본 속성이 정해지지 않아, 사용자가 직접 custom하는 cell이다.
- ```UICollectionViewCell```타입을 따른다.
- Content, SelectedBackground, Background 순서로 존재한다.
- Custom을 하는경우 ```UICollectionViewCell``` 따르는 클래스를 만들어야 한다.

> Custom Cell Class
```swift
import UIKit

class ColorCollectionViewCell: UICollectionViewCell {
    
    @IBOutlet weak var colorView: UIView!
    @IBOutlet weak var hexLabel: UILabel!
    @IBOutlet weak var nameLabel: UILabel!
    
    override func awakeFromNib() {
        super.awakeFromNib()
        
        colorView.clipsToBounds = true
        colorView.layer.cornerRadius = colorView.bounds.width / 2
    }
}
```

> ViewController

```swift
import UIKit

class CustomCellViewController: UIViewController {
    
    let list = MaterialColorDataSource.generateSingleSectionData()
    
    @IBOutlet weak var listCollectionView: UICollectionView!
    
    override func prepare(for segue: UIStoryboardSegue, sender: Any?) {
        
        // type casting
        guard let cell = sender as? UICollectionViewCell else {
            return
        }
        
        guard let indexPath = listCollectionView.indexPath(for: cell) else { // 선택된 cell
            return
        }
        
        let target = list[indexPath.item]
        
        segue.destination.view.backgroundColor = target.color
        segue.destination.title = target.title
    }
    
    override func viewDidLoad() {
        super.viewDidLoad()
    }
}

extension CustomCellViewController: UICollectionViewDataSource {
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return list.count
    }

    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: "cell", for: indexPath) as! ColorCollectionViewCell
        
        let target = list[indexPath.item]
        cell.colorView.backgroundColor = target.color
        cell.hexLabel.text = target.hex
        cell.nameLabel.text = target.title
        
        return cell
    }
}
```

# ViewController
