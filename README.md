# java_10_account
package ch10_ account;

public class Account {
	
	private String ano;    // 계좌번호 
	private String owner;  // 이름 
	private int balance;   // 잔액 
	
	public Account(String ano, String owner, int balance) {
		this.ano = ano;
		this.owner = owner;
		this.balance = balance;
	}

	public String getAno() {
		return ano;
	}

	public void setAno(String ano) {
		this.ano = ano;
	}

	public String getOwner() {
		return owner;
	}

	public void setOwner(String owner) {
		this.owner = owner;
	}

	public int getBalance() {
		return balance;
	}

	public void setBalance(int balance) {
		this.balance = balance;
	}
	
	
		
}
package ch10_extends_interface.account;

import java.util.Scanner;

public class BankApplication {
	
	private static Account [] accountArr = new Account[100];
	private static Scanner scan = new Scanner(System.in);
	
	public static void main(String[] args) {
		 boolean run = true;
		 while(run) {
			 System.out.println("-----------------------");
			 System.out.println("1.계좌생성|2.계좌목록|3.예금|4.출금|5.종료");
			 System.out.println("-----------------------");
			 System.out.println("선택> ");
			 int selectNo = Integer.parseInt(scan.nextLine());
			 if(selectNo ==1 ) {
				 //계좌생성 메소드
				 createAccount();
			 }else if(selectNo ==2) {
				 //계좌목록 출력 메소드
				 accountList();
			 }else if(selectNo ==3) {
				 //예금 메소드
				 deposit();
			 }else if(selectNo ==4) {
				 //출금 메소드
				 withdraw();
			 }else if(selectNo ==5) {
				 run = false;
			 }
		 }
		 System.out.println("프로그램 종료");
	}
	
	//계좌생성하기 
		private static void createAccount() {
			 System.out.println("----------");
			 System.out.println("계좌생성");
			 System.out.println("----------");
			 System.out.print("계좌번호: ");
			 String ano = scan.nextLine();
			 System.out.print("계좌주: ");
			 String owner = scan.nextLine();
			 System.out.println("초기입금금액: ");
			 int balance =Integer.parseInt(scan.nextLine());
			 Account newAccount = new Account(ano, owner, balance);
			 for(int i = 0 ; i < accountArr.length; i++) {
				 if(accountArr[i] == null) {
					 accountArr[i] = newAccount;
					 System.out.println("결과: 계좌가 생성되었습니다.");
					 break;
				 }
			 }
		}
		//계좌 목록보기 
		private static void accountList() {
			System.out.println("-----------");
			System.out.println("계좌목록");
			System.out.println("-----------");
			for(int i = 0 ; i < accountArr.length ; i++) {
				Account accout = accountArr[i];
				if(accout != null) {
					System.out.print(accout.getAno());
					System.out.print("    ");
					System.out.print(accout.getOwner());
					System.out.print("    ");
					System.out.print(accout.getBalance());
					System.out.println();
				}
			}
		}
		// 예금하기 
		private static void deposit() {
			System.out.println("-------------");
			System.out.println("예금");
			System.out.println("-------------");
			System.out.print("계좌번호: ");
			String ano = scan.nextLine();
			System.out.print("예금액: ");
			// 계좌번호로 Account 찾기 
			int money = Integer.parseInt(scan.nextLine());
			Account account = findAccount(ano);
			if(account == null) {
				System.out.println("결과: 계좌가 없습니다.");
				return;
			}
			System.out.println("예금전: " + account.getBalance());
			account.setBalance(account.getBalance() + money);
			System.out.println("결과: 예금이 성공되었습니다.");
			// 예금 후 잔액 출력	
			System.out.println("잔액: " + account.getBalance());
		}
		// 출금하기 
		private static void withdraw() {
			System.out.println("--------------------");
			System.out.println("출금");
			System.out.println("--------------------");
			System.out.print("계좌번호: ");
			String ano = scan.nextLine();
			System.out.print("출금액: ");
			int money = Integer.parseInt(scan.nextLine());
			Account account = findAccount(ano);
			if(account == null) {
				System.out.println("결과: 계좌가 없습니다.");
				return;
			}
			System.out.println("출금전: " + account.getBalance());
			account.setBalance(account.getBalance() - money);
			System.out.println("결과 : 출금이 성공되었습니다.");
			// 예금 출금 후 잔액 출력
			System.out.println("잔액: " + account.getBalance());
		}
		
		//계좌 찾기 
		private static Account findAccount(String ano) {
			Account account = null;
			for(int i = 0 ; i < accountArr.length;i ++) {
				if(accountArr[i] !=null) {
					String dbAno = accountArr[i].getAno();
					// 동일 계좌번호 				
					if(dbAno.equals(ano)) {
						account = accountArr[i];
						break;
					}
				}
			}
			return account;
		}
}
