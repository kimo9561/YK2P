# CollectionView
- grid Layout을 표현해주는 View이다. (인스타그램 돋보기 모양)
- Section과 Item으로 구분되어 있다. 
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


# ViewController
