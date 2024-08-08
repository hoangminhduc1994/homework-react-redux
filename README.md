# homework-react-redux


### 1. State được lưu ở đâu trong ứng dụng React + Redux?

Trong một ứng dụng React + Redux, state được lưu trữ trong một **store** duy nhất do Redux quản lý. Store là một đối tượng JavaScript lưu trữ toàn bộ state của ứng dụng trong một cây (state tree) duy nhất. Điều này giúp đảm bảo rằng state của ứng dụng có một nguồn duy nhất và nhất quán, giúp dễ dàng quản lý và kiểm soát các thay đổi.

Các thành phần (components) của React có thể truy cập state này thông qua việc sử dụng các selectors (các hàm lấy state) và có thể cập nhật state thông qua việc dispatch các actions (hành động). Mỗi action mô tả một loại thay đổi cụ thể mà bạn muốn thực hiện với state, và reducers sẽ xác định cách state cần thay đổi dựa trên các actions đó.

### 2. Điểm mấu chốt (mạnh nhất) của Redux là gì?

Điểm mấu chốt và mạnh nhất của Redux là **cấu trúc dự đoán được** của nó. Redux giúp quản lý state của ứng dụng theo một cách thức rõ ràng và dễ dàng dự đoán, nhờ vào các nguyên tắc sau:

- **Single source of truth (Nguồn sự thật duy nhất):** Tất cả state của ứng dụng được lưu trữ trong một store duy nhất. Điều này giúp đồng bộ hóa mọi thay đổi và đảm bảo rằng các phần khác nhau của ứng dụng có thể dễ dàng truy cập vào cùng một state.

- **State là không thay đổi (Immutable State):** State trong Redux là bất biến (immutable), có nghĩa là nó không thể thay đổi trực tiếp. Thay vào đó, mỗi khi có một sự thay đổi, một state mới sẽ được tạo ra dựa trên state cũ và action được dispatch. Điều này giúp việc theo dõi lịch sử thay đổi của state trở nên dễ dàng hơn và giúp ngăn ngừa lỗi do các thay đổi không mong muốn.

- **Pure functions (Reducers):** Reducers là các hàm thuần túy (pure functions), nghĩa là chúng không có side effects (tác dụng phụ) và luôn trả về cùng một kết quả nếu nhận vào cùng một state và action. Điều này đảm bảo tính nhất quán và dễ dự đoán khi cập nhật state.

- **Khả năng debug tốt (Debuggable):** Với sự hỗ trợ của các công cụ như Redux DevTools, bạn có thể dễ dàng theo dõi và kiểm tra lịch sử của các actions và state trong ứng dụng. Điều này làm cho việc tìm và sửa lỗi trở nên dễ dàng hơn rất nhiều.

### 3. Các middleware thường được chọn để xử lý các lời gọi bất đồng bộ trong Redux là gì?

Trong Redux, middleware là những phần mở rộng cho phép bạn can thiệp vào quá trình dispatch actions. Các middleware thường được sử dụng để xử lý các tác vụ bất đồng bộ trong Redux bao gồm:

- **Redux Thunk:** Đây là một middleware đơn giản nhưng mạnh mẽ, cho phép bạn viết các action creators trả về một hàm thay vì một đối tượng. Hàm này có thể chứa các logic bất đồng bộ như gọi API và sau đó dispatch các actions khác khi tác vụ bất đồng bộ hoàn thành. Redux Thunk rất phù hợp cho các ứng dụng đơn giản hoặc trung bình.

- **Redux Saga:** Một middleware mạnh mẽ hơn Redux Thunk, sử dụng các generator functions để quản lý các side effects như gọi API, quản lý trạng thái, hoặc thực hiện các tác vụ bất đồng bộ khác. Redux Saga cho phép quản lý các side effects phức tạp hơn một cách dễ dàng và rõ ràng. Nó hoạt động dựa trên các "sagas", là những luồng logic bất đồng bộ có thể dễ dàng được kiểm tra và quản lý.

- **Redux Observable:** Đây là một middleware dựa trên RxJS, cho phép bạn sử dụng các "epics" (dòng chảy side effects) để xử lý các tác vụ bất đồng bộ. Redux Observable phù hợp với các ứng dụng cần quản lý các luồng dữ liệu phức tạp và liên tục.

### 4. Redux Thunk được sử dụng để làm gì?

Redux Thunk là một middleware được sử dụng trong Redux để cho phép bạn viết các action creators có thể trả về một hàm thay vì chỉ trả về một đối tượng action thông thường. Điều này rất hữu ích cho việc xử lý các tác vụ bất đồng bộ, chẳng hạn như gọi API, truy vấn cơ sở dữ liệu, hoặc thực hiện các công việc khác mà không thể được thực hiện ngay lập tức.

#### Chức năng chính của Redux Thunk:

- **Thực hiện các tác vụ bất đồng bộ:** Với Redux Thunk, bạn có thể thực hiện các tác vụ bất đồng bộ như gọi API trước khi dispatch một action. Điều này giúp bạn quản lý các quá trình xử lý bất đồng bộ một cách dễ dàng hơn.

- **Điều kiện hóa việc dispatch actions:** Redux Thunk cho phép bạn thêm logic vào việc dispatch actions, chẳng hạn như chỉ dispatch một action trong một số điều kiện nhất định hoặc sau khi một tác vụ khác đã hoàn thành.

### Ví dụ chi tiết về Redux Thunk:
```js
const fetchUserData = () => {
    return async (dispatch) => {
        try {
            dispatch({ type: 'FETCH_USER_DATA_REQUEST' });
            
            const response = await fetch('/api/user');
            const data = await response.json();

            dispatch({ type: 'FETCH_USER_DATA_SUCCESS', payload: data });
        } catch (error) {
            dispatch({ type: 'FETCH_USER_DATA_FAILURE', payload: error });
        }
    };
};
```
