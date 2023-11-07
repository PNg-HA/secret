## 1. Abtract

- Tác giả của bài báo đã nhận thức được những hạn chế của hệ thống kiểm soát truy cập tập trung truyền thống, như rủi ro về rò rỉ thông tin cá nhân, a single point of failure, vấn đề tương thích, không tin cậy và sự hiện diện của các bên thứ ba. Để giải quyết những vấn đề này, tác giả đề xuất một hệ thống kiểm soát truy cập phi tập trung sử dụng công nghệ blockchain.
- Sự phi tập trung của công nghệ blockchain giải quyết vấn đề  a single point of failure, vì cryptography methods đảm bảo reliability của ledger, cơ chế consensus đảm bảo rằng trạng thái của ledger là hợp lệ và giống nhau đối với mọi người tham gia, và smart contract cho phép theo dõi và thực hiện các quyết định kiểm soát truy cập phức tạp. Với automatic enforcement, hệ thống có thể giải quyết các vấn đề về quyền riêng tư, và với automatic enforcement của hợp đồng thông minh, hệ thống không cần bên thứ ba để quản lý kiểm soát truy cập. Quyền riêng tư được nâng cao bằng cách tránh tiết lộ dữ liệu cho các bên thứ ba, đó là nguồn rò rỉ dữ liệu quan trọng.
- Kiến trúc hệ thống được đề xuất dựa trên một blockchain được cấp phép, cho phép hệ thống hoạt động hiệu quả và có khả năng mở rộng hơn. Tác giả cũng cung cấp một phân tích về hiệu suất của việc triển khai hệ thống, bao gồm các cơ chế thống nhất và cơ sở dữ liệu khác nhau. Kết quả cho thấy rằng kiến trúc hệ thống được đề xuất đạt hiệu suất cao và ít tải tính toán, tạo nên một giải pháp thích hợp cho kiểm soát truy cập đáng tin cậy trong các hệ thống phân tán.
- Tóm lại, bài báo đề xuất một hệ thống kiểm soát truy cập dựa trên thuộc tính được phân phối sử dụng blockchain được cấp phép giải quyết những hạn chế của hệ thống kiểm soát truy cập tập trung truyền thống. Kiến trúc hệ thống được đề xuất đạt hiệu suất cao và ít tải tính toán, tạo nên một giải pháp thích hợp cho kiểm soát truy cập đáng tin cậy trong các hệ thống phân tán.

- ## 2. Objectives of the study

### ABAC (attribute-based access control)

- ABAC là một mô hình kiểm soát truy cập mà quyết định quyền truy cập vào tài nguyên dựa trên các thuộc tính (attributes) của các thực thể trong hệ thống. Các thực thể bao gồm người dùng (subjects), tài nguyên (resources), và ngữ cảnh (environment). ABAC tập trung vào việc sử dụng các thuộc tính để xác định các quyền truy cập cụ thể thay vì dựa vào các vai trò cố định hay cấp độ truy cập được định trước.
- Một số khai niệm của ABAC
    1. **Thuộc tính (Attributes)**: Đây là các đặc điểm hoặc thông tin mô tả các thực thể trong hệ thống. Ví dụ về thuộc tính cho người dùng có thể bao gồm tên, vai trò, bộ phận, cấp độ xác minh, hoặc bất kỳ thông tin nào liên quan.
    2. **Chính sách kiểm soát truy cập (Access Control Policies)**: Đây là các quy tắc hoặc luật lệ định nghĩa điều kiện dưới đây truy cập được phép hoặc từ chối. Chính sách kiểm soát truy cập ABAC thường dựa trên các so sánh giữa các thuộc tính của người dùng, tài nguyên và môi trường.
    3. **Chính sách tích hợp (Combining Policies)**: ABAC cho phép kết hợp nhiều chính sách lại với nhau để xác định quyền truy cập cuối cùng. Các kết hợp chính sách có thể sử dụng các toán tử logic như AND, OR, NOT để quyết định quyền truy cập.
    4. **Điểm quyết định chính sách (Policy Decision Point - PDP)**: Là thành phần quyết định cuối cùng xem xét các chính sách kiểm soát truy cập và quyết định xem quyền truy cập có được cấp hay không.
    5. **Điểm thông tin chính sách (Policy Information Point - PIP)**: Là nơi lấy thông tin về thuộc tính của các thực thể và truyền nó cho PDP để đưa ra quyết định.
    6. **Điểm quản lý chính sách (Policy Administration Point - PAP)**: Là nơi quản lý và định nghĩa các chính sách kiểm soát truy cập.

### Hyperledger Fabric

- Tác giả sử dụng Hyperledger Fabric, một nền tảng blockchain được phát triển bởi Linux Foundation, để triển khai hệ thống truy cập kiểm soát. Hyperledger Fabric cung cấp các tính năng như quản lý danh sách thành viên, quyền truy cập và quyền kiểm soát, và khả năng mở rộng.

### Blockchain

- Permissioned blockchain: Tác giả sử dụng blockchain có quyền truy cập để lưu trữ các thuộc tính kiểm soát truy cập và truy vấn quyền truy cập. Blockchain có quyền truy cập chỉ cho phép các thành viên được xác thực tham gia vào mạng và thực hiện các giao dịch.

### JSON

- JavaScript Object Notation (JSON): Tác giả sử dụng định dạng dữ liệu JSON để lưu trữ các thuộc tính của người dùng và tài nguyên trong hợp đồng thông minh. JSON là một định dạng dữ liệu phổ biến và dễ dùng để lưu trữ và truy xuất thông tin.

### Tamper-proof ledger

- Tamper-proof ledger: Tác giả sử dụng một ledger không thể thay đổi để lưu trữ dữ liệu kiểm soát truy cập. Sổ cái này đảm bảo tính toàn vẹn của dữ liệu và không cho phép sửa đổi hay xóa bỏ các giao dịch đã được ghi lại.

## 3. Research Methods

![image](https://github.com/PNg-HA/secret/assets/93396414/c89cac2c-5bfa-4263-af5c-7b2319714870)

- Tác giả sử dụng blockchain Hyperledger Fabric để tạo quyền kiểm soát truy cập cho cả chủ sở hữu tài nguyên và người dùng yêu cầu truy cập. Trong mạng blockchain, cần ít nhất hai nút chấp thuận để tạo sự tin tưởng. Chúng cũng là những người thực thi các hợp đồng thông minh. Khách hàng (Clients) là các hệ thống sử dụng giải pháp này để quản lý kiểm soát truy cập.

### System Architecture

- Hệ thống được thiết kế để cung cấp quản lý kiểm soát truy cập cho các tài nguyên. Người sở hữu tài nguyên và người yêu cầu truy cập đều có quyền kiểm soát và theo dõi quyền truy cập.
- Hệ thống sử dụng mô hình Smart Policys (SPs) để đại diện cho các chính sách kiểm soát truy cập. Các chính sách này được biểu diễn bằng các hợp đồng thông minh được lưu trữ trên blockchain. Mỗi khi có yêu cầu truy cập, hệ thống sẽ thực hiện quá trình đánh giá chính sách dựa trên thông tin về người dùng và quyền truy cập được yêu cầu.
- Hệ thống sử dụng các thành phần Attribute Manager (AM) để quản lý các thuộc tính của các thực thể liên quan trong quá trình kiểm soát truy cập, chẳng hạn như người dùng, tài nguyên và ngữ cảnh môi trường. AM có khả năng cập nhật và truy xuất các giá trị thuộc tính và được tạo ra bởi Attribute Provider (AP).
- Hệ thống cũng sử dụng các thành phần khác như Client, Policy Enforcement Point (PEP), Policy Information Point (PIP), Policy Decision Point (PDP), và Policy Administration Point (PAP). Client là thiết bị yêu cầu truy cập tài nguyên, PEP là thiết bị mạng thực hiện quyết định truy cập, PIP là kho lưu trữ thông tin về người dùng và cung cấp thông tin này cho PDP, PDP là thành phần quyết định cho phép hoặc từ chối truy cập, và PAP là thành phần quản lý chính sách kiểm soát truy cập.

![image](https://github.com/PNg-HA/secret/assets/93396414/906f6085-8293-4c92-9ef4-1eea3fedab83)

## 4. Result

- Đánh giá hiệu suất: Tác giả đã thực hiện các thử nghiệm để đánh giá hiệu suất của hệ thống. Kết quả cho thấy hệ thống có thể xử lý khoảng 270 giao dịch mỗi giây với độ trễ trung bình là 0,54 giây mỗi giao dịch. Điều này cho thấy hệ thống có khả năng xử lý một lượng lớn giao dịch một cách hiệu quả.
- Bảo mật: Hệ thống đã giải quyết các vấn đề về bảo mật và riêng tư mà các hệ thống kiểm soát truy cập tập trung thường gặp phải. Hệ thống cung cấp dữ liệu kiểm tra đáng tin cậy để đảm bảo tính minh bạch và không thể chối bỏ. Tuy nhiên, cần có các biện pháp phòng ngừa bổ sung để đảm bảo không có cách nào khác để truy cập tài nguyên được bảo vệ và đảm bảo rằng cơ sở dữ liệu trạng thái cục bộ không bị sửa đổi hoặc truy cập bởi các quản trị viên hệ thống.
- Ứng dụng thực tế: Tác giả đã triển khai một ứng dụng quản lý truy cập phân tán trong các thư viện số để kiểm tra hiệu quả của hệ thống. Hệ thống đã được xây dựng dựa trên kiến trúc Hyperledger Fabric và các thành phần quản lý truy cập đã được triển khai bằng smart contract. Kết quả thực nghiệm cho thấy hệ thống có khả năng xử lý một lượng lớn giao dịch một cách hiệu quả và đáng tin cậy.
