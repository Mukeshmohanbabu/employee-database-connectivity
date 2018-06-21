# employee-database connectivity
  
  /*
 * To change this license header, choose License Headers in Project Properties.
 * To change this template file, choose Tools | Templates
 * and open the template in the editor.
 */
package com.emp.w3global.controller;

import java.io.IOException;
import java.io.PrintWriter;
import java.sql.Connection;
import java.sql.DriverManager;
import java.sql.PreparedStatement;
import java.sql.ResultSet;
import java.sql.SQLException;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 *
 * @author w3global
 */
public class EmployeeController extends HttpServlet {

    /**
     * Processes requests for both HTTP <code>GET</code> and <code>POST</code>
     * methods.
     *
     * @param request servlet request
     * @param response servlet response
     * @throws ServletException if a servlet-specific error occurs
     * @throws IOException if an I/O error occurs
     */
    protected void processRequest(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html;charset=UTF-8");
        
       String ename =  request.getParameter("ename");
       String deg  =request.getParameter("deg");
       String qualif =request.getParameter("qualif");
       String exp =request.getParameter("exp");
       String skills=request.getParameter("skills");
       
       try
        {
            Class.forName("com.mysql.jdbc.Driver");
            Connection c=DriverManager.getConnection("jdbc:mysql://localhost:3306/home","root","root");
            PreparedStatement p=c.prepareStatement("insert into home values(?,?,?,?,?)");
            p.setString(1,ename);
            p.setString(2,deg);
            p.setString(3,qualif);
            p.setString(4,exp);
            p.setString(5,skills);
            p.executeUpdate();
            System.out.println(1+"row inserted");
            p.close();
            c.close();
            
        }catch(ClassNotFoundException | SQLException e)
        {
                   e.printStackTrace();
        }
       finally{
        
            
       }
        
        
        
        try (PrintWriter out = response.getWriter()) {
            /* TODO output your page here. You may use following sample code. */
            out.println("<!DOCTYPE html>");
            out.println("<html>");
            out.println("<head>");
            out.println("<title>Servlet EmployeeController</title>");            
            out.println("</head>");
            out.println("<head>");
            out.println("<title>Servlet EmployeeController</title>");            
            out.println("<body>");
            out.println("<h1>"+ request.getParameter("ename") + request.getContextPath() + "</h1>");
             out.println("<h1> "+ request.getParameter("deg") + request.getContextPath() + "</h1>");
             out.println("<h1> "+ request.getParameter("qualif") + request.getContextPath() + "</h1>");
              out.println("<h1> "+ request.getParameter("exp") + request.getContextPath() + "</h1>");
               out.println("<h1> "+ request.getParameter("skills") + request.getContextPath() + "</h1>");
            out.println("</body>");
            out.println("</html>");
        }
    }
    
    

    // <editor-fold defaultstate="collapsed" desc="HttpServlet methods. Click on the + sign on the left to edit the code.">
    /**
     * Handles the HTTP <code>GET</code> method.
     *
     * @param request servlet request
     * @param response servlet response
     * @throws ServletException if a servlet-specific error occurs
     * @throws IOException if an I/O error occurs
     */
    @Override
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        //processRequest(request, response);
        /*
        response.setContentType("text/html:chatacter-utf-8");
        try(printWriter out=response.getWriter()){
            ename=request.getParameter(txtename);
            deg=request.getParameter(txtdeg);
            qualif=request.getParameter(txtqualif);
            exp=request.getParameter(txtexp);
            skills=request.getParameter(txtskills);
            
           Class.forName("com.mysql.jdbc.Driver");
           conn=createStaement("")
           
            
        }
        */
        
        try
        {
            Class.forName("com.mysql.jdbc.Driver");
            Connection c=DriverManager.getConnection("jdbc:mysql://localhost:3306/home","root","root");
            PreparedStatement p=c.prepareStatement("select * from home");
            ResultSet rs = p.executeQuery();
          //*
            while(rs.next()){
                PrintWriter out = response.getWriter();
                out.println("<h3> test" +rs.getString("name")+rs.getString("deg")+rs.getString("qualif")+ rs.getString("exp")+rs.getString("skills") + "</h3>");
               
                
            }
        rs.close();
            p.close();
            c.close();
            
            
        } catch(IOException | ClassNotFoundException | SQLException e){
        }        
    }

    /**
     * Handles the HTTP <code>POST</code> method.
     *
     * @param request servlet request
     * @param response servlet response
     * @throws ServletException if a servlet-specific error occurs
     * @throws IOException if an I/O error occurs
     */
    
    @Override
    protected void doPost(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        processRequest(request, response);
    }

    /**
     * Returns a short description of the servlet.
     *
     * @return a String containing servlet description
     */
    @Override
    public String getServletInfo() {
        return "Short description";
    }// </editor-fold>

}
