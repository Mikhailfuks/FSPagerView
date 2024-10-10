import UIKit
import FSPagerView

class ViewController: UIViewController, FSPagerViewDelegate, FSPagerViewDataSource {

  @IBOutlet weak var pagerView: FSPagerView!

  override func viewDidLoad() {
    super.viewDidLoad()

    // Set up FSPagerView
    pagerView.delegate = self
    pagerView.dataSource = self
    pagerView.register(FSPagerViewCell.self, forCellWithReuseIdentifier: "cell")
    pagerView.automaticSlidingInterval = 4.0 // Set automatic sliding interval (in seconds)

    // Customize appearance (optional)
    pagerView.transformer = FSPagerViewTransformer(type: .linear)
    pagerView.interitemSpacing = 10.0
  }

  // FSPagerViewDataSource methods
  func numberOfItems(in pagerView: FSPagerView) -> Int {
    return 5 // Number of items in the pager
  }

  func pagerView(_ pagerView: FSPagerView, cellForItemAt index: Int) -> FSPagerViewCell {
    let cell = pagerView.dequeueReusableCell(withReuseIdentifier: "cell", at: index)
    cell.textLabel?.text = "Page (index + 1)" // Customize cell content
    cell.backgroundColor = .randomColor() // Customize cell background color
    return cell
  }

  // FSPagerViewDelegate methods
  func pagerView(_ pagerView: FSPagerView, didSelectItemAt index: Int) {
    print("Selected page: (index + 1)")
  }

  func pagerViewWillEndDragging(_ pagerView: FSPagerView, targetIndex: Int) {
    print("Will end dragging at page: (targetIndex + 1)")
  }

  func pagerViewDidEndDragging(_ pagerView: FSPagerView, targetIndex: Int) {
    print("Did end dragging at page: (targetIndex + 1)")
  }
}

// Helper function to generate random colors
extension UIColor {
  static func randomColor() -> UIColor {
    let red = CGFloat.random(in: 0...1)
    let green = CGFloat.random(in: 0...1)
    let blue = CGFloat.random(in: 0...1)
    return UIColor(red: red, green: green, blue: blue, alpha: 1.0)
  }
}
