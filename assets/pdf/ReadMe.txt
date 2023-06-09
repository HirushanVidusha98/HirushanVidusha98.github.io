package paper;

import java.io.File;

import javax.xml.parsers.DocumentBuilderFactory;
import javax.xml.parsers.ParserConfigurationException;
import javax.xml.transform.Transformer;
import javax.xml.transform.TransformerException;
import javax.xml.transform.TransformerFactory;
import javax.xml.transform.TransformerFactoryConfigurationError;
import javax.xml.transform.dom.DOMSource;
import javax.xml.transform.stream.StreamResult;

import org.w3c.dom.Attr;
import org.w3c.dom.Document;
import org.w3c.dom.Element;

public class Q1 {
	
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
	private static final String GENDER_NODE = "Gender";
	private static final String ADDRESS_NODE = "Address";
	private static final String NAME = "Nimal Perera";
	private static final String GENDER_VALUE = "Male";
	private static final String INITIALS = "Initials";
	private static final String INITIALS_VALUE = "D. D.";

	public static void main(String[] args) throws ParserConfigurationException, TransformerFactoryConfigurationError, TransformerException {
		// TODO Auto-generated method stub
		Q1 q = new Q1();
		q.buildXmlFile();
	}
	

	public Document createDocument() throws ParserConfigurationException {
		return DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument();
	}
	

	public Element createElement(Document doc, String ElemntName) {
		return doc.createElement(ElemntName);
	}
	

	public Attr createAttribute(Document doc, String type, String value) {
		Attr attribute = doc.createAttribute(type);
		attribute.setValue(value);
		return attribute;
	}
	
	public Element appenChilds(Element element, Document doc, String textNode) {
		element.appendChild(doc.createTextNode(textNode));
		return element;
	}
	
	public Element setAttributeForElement(Element element, Attr attribute) {
		element.setAttributeNode(attribute);
		return element;
	}
	

	public void transformToXml(Document doc) throws TransformerFactoryConfigurationError, TransformerException {
		Transformer transformer = TransformerFactory.newInstance().newTransformer();
		DOMSource domsource = new DOMSource(doc);
		transformer.transform(domsource, new StreamResult(new File(XML_FILE)));
		transformer.transform(domsource,new StreamResult(System.out));
	}
	

	public void buildXmlFile() throws ParserConfigurationException, TransformerFactoryConfigurationError, TransformerException {
		
		Document doc = createDocument();
		
		Element employeeElement = setAttributeForElement(createElement(doc, "Employee"), createAttribute(doc, "Gender", "Male"));
		
		
		
		employeeElement.appendChild(appenChilds(setAttributeForElement(setAttributeForElement(createElement( doc, "Address"), createAttribute( doc, "No", "15/3")), createAttribute( doc, "Street", "Avenue street")),  doc, "Nalake"));
		
		doc.appendChild(createElement(doc, "School")).appendChild(createElement(doc, "Studnet")).appendChild(employeeElement);
		
		transformToXml(doc);
	}
}





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
