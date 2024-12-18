# FOOD-ORDERING-SYSTEM-USING-JAVA
import java.awt.*; 

import java.awt.event.*; 

import java.util.ArrayList; 

public class FoodOrderingSystem extends Frame implements ActionListener { 

 // Components for the system 

 Label labelMenu, labelOrder, labelName, labelAddress, labelTotal; 

 Checkbox pizza, burger, pasta, fries; 

 TextField nameField, addressField, totalField; 

 TextArea orderArea; 

 Button orderButton, resetButton; 

 // Prices of items 

 final int PIZZA_PRICE = 250; 

 final int BURGER_PRICE = 150; 

 final int PASTA_PRICE = 200; 

 final int FRIES_PRICE= 100; 

 public FoodOrderingSystem() { 

 // Setting up the Frame 

 setTitle("Food Ordering 

System"); 

 setSize(400, 600); 

 setLayout(null); 

 // Menu section 

 labelMenu = new Label("Select items from the menu:"); 

 labelMenu.setBounds(50, 50, 200, 30); 

 add(labelMenu); 
pizza = new Checkbox("Pizza - rs250"); 

 pizza.setBounds(50, 90, 150, 30); 

 add(pizza); 

 burger = new Checkbox("Burger - rs150"); 

 burger.setBounds(50, 130, 150, 30); 

 add(burger); 

 pasta = new Checkbox("Pasta - rs200"); 

 pasta.setBounds(50, 170, 150, 30); 

 add(pasta); 

 fries = new Checkbox("Fries - rs100"); 

 fries.setBounds(50, 210, 150, 30); 

 add(fries); 

 // Order summary section 

 labelOrder = new Label("Your Order:"); 

 labelOrder.setBounds(50, 250, 100, 30); 

 add(labelOrder); 

 orderArea = new TextArea(); 

 orderArea.setBounds(50, 290, 300, 100); 

 orderArea.setEditable(false); 

 add(orderArea); 

 // Customer details 

 labelName = new Label("Name:"); 

 labelName.setBounds(50, 400, 50, 30); 

 add(labelName); 

nameField = new TextField(); 

 nameField.setBounds(120, 400, 200, 30); 

 add(nameField); 

 labelAddress = new Label("Address:"); 

 labelAddress.setBounds(50, 440, 70, 30); 

 add(labelAddress); 

 addressField = new TextField(); 

 addressField.setBounds(120, 440, 200, 30); 

 add(addressField); 

 // Total section 

 labelTotal = new Label("Total:"); 

 labelTotal.setBounds(50, 480, 50, 30); 

 add(labelTotal); 

 totalField = new TextField(); 

 totalField.setBounds(120, 480, 100, 30);

 totalField.setEditable(false); 

 add(totalField); 

 // Buttons 

 orderButton = new Button("Place Order"); 

 orderButton.setBounds(50, 530, 100, 30); 

 orderButton.addActionListener(this); 

 add(orderButton); 

 resetButton = new Button("Reset"); 

 resetButton.setBounds(180, 530, 100, 30); 

resetButton.addActionListener(this); 

 add(resetButton); 

 // Frame close operation 

 addWindowListener(new WindowAdapter() {

 public void windowClosing(WindowEvent e) { 

 dispose(); 

 } 

 }); 

 setVisible(true); 

 } 

 @Override 

 public void actionPerformed(ActionEvent e) { 

 if (e.getSource() == orderButton) { 

 // Calculate total and display order 

 int total = 0; 

 ArrayList<String> items = new ArrayList<>(); 

 if (pizza.getState()) { 

 total += PIZZA_PRICE; 

 items.add("Pizza - rs250"); 

 } 

 if (burger.getState()) { 

 total += BURGER_PRICE; 

 items.add("Burger - rs150"); 

 } 

 if (pasta.getState()) { 

 total += PASTA_PRICE;
items.add("Pasta - rs200"); 

 } 

 if (fries.getState()) { 

 total += FRIES_PRICE; 

 items.add("Fries - rs100"); 

 } 

String name = nameField.getText(); 

 String address = addressField.getText(); 

 if (name.isEmpty() || address.isEmpty()) { 

 orderArea.setText("Please enter your Name and Address."); 

 return; 

 } 

 // Display selected items in orderArea 

 orderArea.setText(String.join("\n", items)); 

 totalField.setText("rs" + total); 

 // Show confirmation dialog 

 if (showConfirmDialog(items, total, name, address)) { 

 showSuccessDialog(name, items, total, address); 

 } else { 

 orderArea.setText("Order Cancelled."); 

 } 

 } else if (e.getSource() == resetButton) { 

 // Reset all fields 

 pizza.setState(false); 

 burger.setState(false); 

 pasta.setState(false); 

fries.setState(false); 

 orderArea.setText(""); 

 nameField.setText(""); 

 addressField.setText(""); 

 totalField.setText(""); 

 } 

 } 

 private boolean showConfirmDialog(ArrayList<String> items, int total, String name, 

String address) { 

 Dialog confirmDialog = new Dialog(this, "Confirm Order", true); 

 confirmDialog.setSize(300, 200); 

 confirmDialog.setLayout(new GridLayout(5, 1)); 

Label message = new Label("Confirm your order:"); 

Label details = new Label("Order Summary:\n" + 

 String.join(", ", items) + "\nTotal: rs" + total + 

 "\nName: " + name + "\nAddress: " + address); 

Button confirm = new Button("Confirm"); 

 Button cancel = new Button("Cancel"); 

 confirmDialog.add(message); 

 confirmDialog.add(details); 

 confirmDialog.add(confirm); 

 confirmDialog.add(cancel); 

 final boolean[] confirmed = {false}; 

 confirm.addActionListener(e -> { 

 confirmed[0] = true; 

 confirmDialog.dispose(); 

}); 

 cancel.addActionListener(e -> confirmDialog.dispose()); 

 confirmDialog.setVisible(true); 

 return confirmed[0]; 

 } 

 private void showSuccessDialog(String name, ArrayList<String> items, int total, String 

address) { 

 Dialog successDialog = new Dialog(this, "Order Successful", true); 

 successDialog.setSize(300, 200); 

 successDialog.setLayout(new GridLayout(4, 1)); 

 Label message = new Label("Thank you for your order, " + name + "!"); 

 Label summary = new Label("Order Summary: " + String.join(", ", items)); 

 Label deliveryInfo = new Label("Your food will be delivered to: " + address); 

 Button okButton = new Button("OK"); 

 successDialog.add(message); 

 successDialog.add(summary); 

 successDialog.add(deliveryInfo); 

 successDialog.add(okButton); 

 okButton.addActionListener(e -> successDialog.dispose()); 

successDialog.setVisible(true); 

}

public static void main(String[] args) { 

 new FoodOrderingSystem(); 

 } 

}
