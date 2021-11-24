package test;

import java.awt.event.ComponentAdapter;
import java.awt.event.ComponentEvent;
import java.util.Vector;

import javax.swing.JButton;
import javax.swing.JComboBox;
import javax.swing.JFrame;
import javax.swing.JLabel;
import javax.swing.JPanel;
import javax.swing.JScrollPane;
import javax.swing.JSplitPane;
import javax.swing.JTable;
import javax.swing.JTextField;
import javax.swing.table.DefaultTableModel;


	public class UI extends JFrame
	{
		private Operation oper=new Operation();
		private JTable table=new JTable();//表格
		private DefaultTableModel dtm=new DefaultTableModel();//表格模式
		private Vector colName=new Vector();//表格的表头信息
		private JComboBox com_type=new JComboBox();//类型的下拉框
		private JTextField txt_money=new JTextField();//金额的文本框
		private JTextField txt_remark=new JTextField();//备注的文本框
		private JTable setTable()
		{
			colName.add("流水账号");
			colName.add("类型");
			colName.add("金额");
			colName.add("日期");
			colName.add("备注");
			Vector data=oper.select();
			dtm.setDataVector(data, colName);
			table.setModel(dtm);
			return table;
		}
		public JPanel setInfo()
		{
			JPanel jp=new JPanel();
			jp.setLayout(null);
			JLabel lable_type=new JLabel("类型");
			lable_type.setBounds(100,50,30,30);
			jp.add(lable_type);
			com_type.setBounds(150, 50,60,30);
			com_type.addItem("收入");
			com_type.addItem("支出");
			jp.add(com_type);
			
			JLabel lable_money=new JLabel("金额");
			lable_money.setBounds(250,50,30,30);
			jp.add(lable_money);
			txt_money.setBounds(300,50,60,30);
			jp.add(txt_money);
			
			JLabel lable_remark=new JLabel("备注");
			lable_remark.setBounds(400,50,30,30);
			jp.add(lable_remark);
			txt_remark.setBounds(450,50,60,30);
			jp.add(txt_remark);
			
			JButton but_add=new JButton("新增");
			but_add.setBounds(100,100,60,30);
			jp.add(but_add);
			
			JButton but_update=new JButton("修改");
			but_update.setBounds(200,100,60,30);
			jp.add(but_update);
			
			JButton but_del=new JButton("删除");
			but_del.setBounds(300,100,60,30);
			jp.add(but_del);
			
			return jp;		
		}
	public void init()
	{
		//带滚动条的容器，放表格
		JScrollPane jp=new JScrollPane(setTable());
		//带分割线的容器，放表格和编辑界面
		JSplitPane pan=new JSplitPane(JSplitPane.VERTICAL_SPLIT,jp,setInfo());
		pan.addComponentListener(new ComponentAdapter()
				{
			        public void componentResized(ComponentEvent e)
			        {
			        	pan.setDividerLocation(0.6);//分割比例
			        }
				
	            });
		this.add(pan);
	}	
	
	public UI()
	{
		super("欢迎使用");
		this.setBounds(80,80,600,500);
		this.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		init();
	}
	
	public static void main(String[] args)
	{
		new UI().setVisible(true);
	}
}
    

