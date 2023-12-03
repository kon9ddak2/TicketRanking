### Documentation is included in the Documentation folder ###
[과제: 일간 공연랭킹 리포트 작성]
- 예스24티켓 공연 카테고리 리스트를 가져옴
- 각 공연 카테고리별로 1~50위 랭킹 데이터 추출
- 엑셀에 카테고리별 시트를 추가하여 결과 파일 생성 (티켓랭킹_yyyyMMdd xlsx)

[작업내용]
1. 선처리:
- Que는 사용하지 않을 예정으로 TransactionItem 변수타입 queueitem을 String으로 변경, 
- GetTransactionData workflow에서 Get transaction Item 커맨드아웃 처리
- Process Transaction > Set Transaction Status에서 각 예외처리의 Queue상태변경 부분 커맨드아웃 처리

2. 작업순서:
- yes24티켓랭킹 접속, 카테고리정보 가져오기
- 카테고리별로 일간 랭킹 정보 스크래핑
- 스크래핑한 랭킹 정보 카테고리별 시트로 만들어 엑셀파일로 저장
- VBA로 보고서 형태로 스타일 적용 
  (Process딘계에서 시트생성될 때마다 VBA적용시 반복작업에 영향을 줄 것으로 판단되어 
  End단계에서 VBA실행하도록 함)

[Config파일]
URL : http://ticket.yes24.com/New/Rank/Ranking.aspx (예스24티켓 랭킹페이지 주소)
ResultFolderPath : Data/Output (작업결과파일_폴더경로)
FileName: 티켓랭킹_{0}.xlsx (결과파일명)

### REFrameWork Template ###
**Robotic Enterprise Framework**


### How It Works ###

1. **INITIALIZE PROCESS**
[초기화]
- Kill Process (엑셀, 크롬)
- 카테고리 list변수 선언
  TransactionItem으로 이용 
   Invoke: GetData.xaml
- 예스24티켓 접속 (Open Browser)
- 결과파일폴더 초기화 
   Invoke: PathCheck.xaml

2. **GET TRANSACTION DATA**
 [Transaction Data설정]
- Get Transaction Data : liCategory 수 만큼 반복

3. **PROCESS TRANSACTION**
[데이터추출 및 처리]
- 각 카테고리별로 스크래핑 반복
- 카테고리별 엑셀 시트 생성

4. **END PROCESS**
 [종료처리]
- 엑셀  VBA 적용
- close tab 


### For New Project ###

1. Check the Config.xlsx file and add/customize any required fields and values
2. Implement InitiAllApplications.xaml and CloseAllApplicatoins.xaml workflows, linking them in the Config.xlsx fields
3. Implement GetTransactionData.xaml and SetTransactionStatus.xaml according to the transaction type being used (Orchestrator queues by default)
4. Implement Process.xaml workflow and invoke other workflows related to the process being automated
