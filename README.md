# akhm
hibernate coding
package com.akhm.client;

import java.util.HashSet;
import java.util.Scanner;
import java.util.Set;

import org.hibernate.Session;
import org.hibernate.Transaction;

import com.akhm.dao.model.PhoneNumberTl;
import com.akhm.dao.model.User;
import com.akhm.dao.util.HibernateUtil;

public class OneToManyTest {
	public static void main(String[] args) {
		Scanner sc=new Scanner(System.in);
		System.out.println("enter first name");
		String firstName=sc.nextLine();
		System.out.println("enter last name");
		String lastName=sc.nextLine();
		System.out.println("enter how many phone numbers");
		int count=Integer.parseInt(sc.nextLine());
		Set<PhoneNumberTl> phoneNumbers=new HashSet<PhoneNumberTl>();
		for(int i=0;i<count;i++)
		{
			System.out.println("enter phone number");
			Long phoneNumber=Long.valueOf(sc.nextLine());
			System.out.println("enter phone type");
			String phoneType=sc.nextLine();
			
			PhoneNumberTl phoneNumberTl=new PhoneNumberTl();
			phoneNumberTl.setPhoneNumber(phoneNumber);
			phoneNumberTl.setPhoneNumberType(phoneType);
			phoneNumbers.add(phoneNumberTl);
		}
		
		User user=new User();
		user.setFirstName(firstName);
		user.setLastName(lastName);
		user.setPhoneNumbers(phoneNumbers);
		
		Session session=HibernateUtil.getSession();
		Transaction tx=session.beginTransaction();
		Integer userId=(Integer)session.save(user);
		System.out.println("user Id is"+userId);
		tx.commit();
		HibernateUtil.closeSession();
		
	}
}
