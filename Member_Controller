package org.Salody.controller;


import javax.servlet.http.HttpSession;

import org.Salody.DTO.memberDTO;
import org.Salody.Service.MemberService;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;
import org.springframework.web.servlet.mvc.support.RedirectAttributes;

@Controller
public class MemberController {
	private static final Logger logger = LoggerFactory.getLogger(MemberController.class);
	@Autowired
	MemberService mservice;
	
	//회원가입페이지
	@RequestMapping(value="/Member_Join", method = RequestMethod.GET)
	public void Getwrite() {
		logger.info("write");
	}
	//회원가입버튼을 눌렀을때 (Insert)
	@RequestMapping(value="/write", method= RequestMethod.POST)
	public String Postwrite(memberDTO mdto) {
		mservice.Postwrite(mdto);
		return "redirect:/";
	}
	//Mypage 화면 뿌려주기(Select)
	@RequestMapping(value = "/Member_Mypage", method = RequestMethod.GET)
	public void Mypage(memberDTO mdto, Model model) {
		model.addAttribute("Mypage", mservice.Mypage(mdto));
	}
	//수정화면(Update) - Mypage 뿌려준거 똑같이 뿌려주기(Select)
	@RequestMapping(value="/Member_Update", method =RequestMethod.POST)
	public void GetUpdate(memberDTO mdto, Model model) {
		logger.info("mdto="+mdto);
		model.addAttribute("Mypage",mservice.Mypage(mdto));
	}
	
	//수정버튼눌렀을때 최종 Update
	@RequestMapping(value = "/Member_Update2", method=RequestMethod.POST)
	public String Update(memberDTO mdto, RedirectAttributes rttr) {
		mservice.Update(mdto);
		logger.info("mdto2="+mdto);
		rttr.addAttribute("id",mdto.getId()); //"변수명","값"
		return "redirect:/Member_Mypage";
		
	}
	
	//탈퇴버튼눌렀을때 최종 Delete
	@RequestMapping(value = "/Member_Delete", method=RequestMethod.POST)
	public void Delete(memberDTO mdto, HttpSession session) {
		session.invalidate();
		mservice.Delete(mdto);
	}
	
	
	
	
	
	
	//로그인
	@RequestMapping(value = "/Member_Login", method = RequestMethod.GET)
	public void memberlogin() {
	}
	@RequestMapping(value = "/Member_LoginPost", method = RequestMethod.POST)
	public String mlogin(memberDTO mdto, RedirectAttributes rttr,HttpSession session) {
	
		memberDTO result=mservice.mlogin(mdto);
		logger.info("abcd");
		if(result==null) {
			//rttr.addAttribute("check", "fail");
			rttr.addFlashAttribute("check", "fail");
			return "redirect:/Member_Login";
		}else {
			logger.info("session 값이 있으면");
			session.setAttribute("loginId", result.getId());
			logger.info("session 값="+session.getAttribute("loginId"));
			return "redirect:/";
		} 
	}
	// 로그아웃 링크를 클릭했을 때
	@RequestMapping(value = "/Logout", method = RequestMethod.GET)
	public String mlogout(HttpSession session) {
		// session에 저장되어 있는 값을 제거
		session.invalidate();
		return "redirect:/Member_Login";
	}
}
