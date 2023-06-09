
IntStream.iterate(0, i->i+1).limit(10).forEach(i->System.out.println("Thread " + i))

Arrays.asList(stringArray).forEach(p->System.out.println(p));

double total = listofcpoint.stream().mapToDouble(Double::doubleValue).sum();

IntStream.iterate(1, i->i+1).limit(5).forEach(i->{IntStream.iterate(1, j->j+1).limit(5).forEach(j->System.out.print(j));System.out.println();});



package FinalT;

public class NewThread {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		new Thread(
				new Runnable() {

					@Override
					public void run() {
						// TODO Auto-generated method stub
						System.out.println("Old way of thread thread ");
						
					}}).start();;
					
					new Thread(()->System.out.println("New way of thread thread")).start();
	}

}

...........................................................

package Paper;

import java.io.File;

import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.parsers.ParserConfigurationException;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerConfigurationException;
import javax.xml.transform.TransformerException;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.TransformerFactoryConfigurationError;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;

import org.w3c.dom.Attr;
import org.w3c.dom.Document;
import org.w3c.dom.Element;

public class Quesction1 {

private static final String XML_FILE = "students.xml";
private static final String ADDRESS = "No:116/2, Avenue Street, Colombo";
private static final String STREET = "Street";
private static final String STREET_VALUE = "Avenue Street";
private static final String NO = "116/2";
private static final String NO_ATTRIB = "No";
private static final String NAME_NODE = "Name";
private static final String EMPLOYEE_NODE = "Employee";
private static final String SCHOOL_NODE = "School";
private static final String STUDENT_NODE = "Students";
private static final String GENDER = "Gender";
private static final String ADDRESS_NODE = "Address";
private static final String NAME = "Nimal Perera";
private static final String GENDER_VALUE = "Male";
private static final String INITIALS = "Initials";
private static final String INITIALS_VALUE = "D. D.";


	public static void main(String[] args) throws ParserConfigurationException, TransformerFactoryConfigurationError, TransformerException {
		// TODO Auto-generated method stub
		Quesction1 q1 = new Quesction1(); // create object
		q1.buildXmlFile();
	}
	
	public Document createDocument() throws ParserConfigurationException {
		return DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument();
	}
	
	public Element createElement(Document doc,String ElementName) {
		return doc.createElement(ElementName);
	}
	
	public Attr createAttribute(Document doc, String type, String value) {
		Attr attribute = doc.createAttribute(type);
		attribute.setValue(value);
		
		return attribute;
	}
	
	public Element appendChilds(Document doc,Element element, String textnode) {
		element.appendChild(doc.createTextNode(textnode));
		return element;
	}
	
	public Element setAttributeForElement(Element element, Attr attribute) {
		element.setAttributeNode(attribute);
		return element;
	}
	
	public void transformToXml(Document doc) throws TransformerFactoryConfigurationError, TransformerException {
		Transformer transformer = TransformerFactory.newInstance().newTransformer();
		DOMSource domsource = new DOMSource(doc);
		transformer.transform(domsource, new StreamResult(new File("student.xml")));
		transformer.transform(domsource, new StreamResult(System.out));
	}
	

	public void buildXmlFile() throws ParserConfigurationException, TransformerFactoryConfigurationError, TransformerException  {
		Document doc = createDocument();
		
		Element employeeElement = setAttributeForElement(createElement(doc,"Employee"), createAttribute(doc,"Gender", "Male") );
		
		employeeElement.appendChild(appendChilds(doc,setAttributeForElement(createElement(doc,"Name"), createAttribute(doc,"Initials", "S.A")),"Nalaka Dissanayake"));
		employeeElement.appendChild(appendChilds(doc,setAttributeForElement(setAttributeForElement(createElement(doc,"Address"), createAttribute(doc, "No", "115/2")), createAttribute(doc, "Street", "Avenue Street")), "N0 435, kandy road, Malabe"));
		//employeeElement.appendChild(appendChilds(doc,setAttributeForElement(createElement(doc,"Address"),createAttribute(doc,"Street", "Avenue Street")),"N0 435, kandy road, Malabe"));

		doc.appendChild(createElement(doc,"School")).appendChild(createElement(doc,"Student")).appendChild(employeeElement);
		
		transformToXml(doc);
	
	}
}





............................................................


package Regular;

import java.util.ArrayList;
import java.util.List;

interface ITrafficService{
	public String checkSpeed(List<Double> listOfCheckPoints);
}
public class Question2 {
	public static void main(String[] args) {
		
		ITrafficService itrafficService = listOfCheckPoints ->{
			//double total = 0;
		/*	for (Double speed : listOfCheckPoints) {
				total= total+speed;
			} */
			double total = listOfCheckPoints.stream().mapToDouble(Double:: doubleValue).sum();
			
			double averageSpeed = total/listOfCheckPoints.size();
			
			if(averageSpeed >= 100.0) {
				return "Issue Fine";
			}else if ((averageSpeed<100.0)&& (averageSpeed >= 80.0)) {
				return "Warning Msg";
			}else if ((averageSpeed<80.0)&& (averageSpeed >= 50.0)) {
				return "Good Speed";
			}else if ((averageSpeed<50.0)&& (averageSpeed >= 30.0)) {
				return "Normal";
			}else {
				return "Slow";
			}
		};
		ArrayList<Double> speedInCheckPoint = new ArrayList<>();
		speedInCheckPoint.add(20.0);
		speedInCheckPoint.add(30.0);
		speedInCheckPoint.add(60.0);
		speedInCheckPoint.add(80.0);
		speedInCheckPoint.add(100.0);
		speedInCheckPoint.add(120.0);
	
		String result = itrafficService .checkSpeed(speedInCheckPoint);
		System.out.println("Vehicle average status is in = " + result);
	}
}

.....................................................................................

package Regular;

import java.util.ArrayList;
import java.util.List;

interface IReference{
	void displayFruits();
}
public class Q1cAns {
	
	public void displayFruits() {
		List<String> fruits = new ArrayList<String>(); 
		fruits.add("Banana");
		fruits.add("Mange");
		fruits.add("Orange");
		fruits.add("Apple");
		fruits.forEach((fruit) ->System.out.println(fruit));
	}
	public static void main(String[] args) {
	
		Q1cAns first = new Q1cAns();
		IReference ireference =() ->{
			first.displayFruits();
		};
		ireference.displayFruits();
	}
}


.....................................................................
package Regular;

import java.util.stream.IntStream;

public class Q1b  {

	public static void main(String[] args) {
		
		Runnable r1 =() ->{
		
		IntStream.rangeClosed(1, 5).forEach(row ->{
			IntStream.rangeClosed(1, 5).forEach(column -> System.out.print(column));
			
				System.out.println(); 
			});
		   	//for (int row =1; row<=5;row++) {
			//	for(int column =1; column<=5; column++) {
			//		System.out.print(column);
			//	}	
			//}
			//};
		};
	new Thread(r1).start();
	}
}

................................................................................

package main;

import java.util.ArrayList;

public class Main {
	public static void main(String[] args) {
		ArrayList<Integer> list = new ArrayList<>();
		
		Runnable ThreadConsumer = () ->{
			while(true) {
				synchronized(list) {
					if (list.isEmpty()) {
						try {
							list.wait();
						} catch (InterruptedException e) {
							// TODO Auto-generated catch block
							e.printStackTrace();
						}
					}else {
						System.out.println("Conusmer Start" );
						int value= list.remove(0);
						System.out.println("Consumer remove ="+ value+ "from list");
						list.notify();
					}
				}
			}
		};
		Runnable ThreadProducer = ()->{
			synchronized (list) {
				int value = 0;
					while (true) {
						System.out.println("Producer started");
						try {
							value += 10;
							list.add(value);
							System.out.println("Producer adding = " + value + " to List");
							list.wait();
							Thread.sleep(1000);
							
						}catch (InterruptedException e) {
							e.printStackTrace();
		}
						list.notify();
						System.out.println("Elements in List = " + list);
					}
			}
		}; 
		Thread producer = new Thread (ThreadProducer); 
		Thread consumer = new Thread (ThreadConsumer); 
		producer.start();
		consumer.start();
	}

}













